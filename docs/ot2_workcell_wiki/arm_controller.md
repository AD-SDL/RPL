# Purpose
The purpose behind the arm_controller / arm_client packages (armManager, armTransferHandler, publish_arm_state_api, transfer_api) is to provide a way to communicate with the arm through a ROS 2 network and easily attach any arm protocols with little to no modification. It is also to provide a clean and easy-to-use API for other packages to easily obtain information about the arm, request transfers, and obtain the current state of the arm. 

# Driver creation specifications 
**Location:** Must be in a package called `arm_driver_pkg` and functions must be in the file `arm_driver.py` and setup with the ROS2 build format.  
## Function Descriptions 
arm_transfer(<job (Not currently in use)>, <robot 1 (transfer from)>, <robot 2 (transfer to)>) - This function will implement the arm transfer from robot1 to to robot2. The function should return an output_msg for the ROS layer to receive. 

# Files  
**arm_controller/**   
&nbsp;&nbsp;  **arm_controller/**  
&nbsp;&nbsp;&nbsp;&nbsp;    armManager.py (Manages the state of the arm)  
&nbsp;&nbsp;&nbsp;&nbsp;    armTransferHandler.py (Manages transfer service)  
&nbsp;&nbsp;  **launch/**  
&nbsp;&nbsp;&nbsp;&nbsp;    arm_bringup.launch.py (Launches the arm)  
  
**arm_client/**  
&nbsp;&nbsp;  **arm_client/**  
&nbsp;&nbsp;&nbsp;&nbsp;    transfer_api.py (An api for other OT2s to use to transfer items)  
&nbsp;&nbsp;&nbsp;&nbsp;    publish_arm_state_api.py (api to publish its state to a manager)  

# Dependencies 
This section discusses the package dependencies. 
## arm_controller 
dependencies are: 
1. [workcell_interfaces](workcell_interfaces)
2. [ot2_workcell_manager_client](ot2_workcell_manager)
3. [arm_client](arm_controller)
4. [ot2_client](ot2_controller)

## Note!!! The below is not up to date!
## arm_client
dependencies are: 
1. [workcell_interfaces](workcell_interfaces)
2. [ot2_workcell_manager_client](ot2_workcell_manager)

# Arm Bring up (launch arm) 
1. source ~/ot2_ws/install/setup.bash
2. ros2 launch arm_controller arm_bringup.launch.py

# File Documentation
This section discusses the various APIs available for arm_controller. 
## transfer_api.py usage 
#### Functions - 
1. load_transfer(self, from_name_or_id, to_name_or_id, item, arm_name_or_id)
2. _load_transfer(args)

#### Function Explanations - 
load_transfer(...) explanation:  This function allows a OT-2 node to add itself to a transfer queue, when both sides, <from_name_or_id> <to_name_or_id>, are both in the queue it signals that both OT-2s are halted and ready to receive a transfer. Once that is the case, the arm will then execute a transfer protocol moving the <item> between the 2 OT-2s. It will then let the caller (one of the OT-2s) know that the transfer was complete, and put an entry in the completed queue so that when the second OT-2 calls it will also know that the transfer was completed. Both OT-2s during the transfer period are spinning and not doing any work in order to prevent a possible collision with the arm during the transfer period. Errors are caught by the **retry** function (retry_api in ot2_workcell_manager). This is gone over in the _load_transfer(...) explanation.  

_load_transfer(...) explanation: This function is a middleman function, in other words, its job is to provide a segway to the load_transfer(...) function. This allows this function to be run in a retry_function (retry_api in mastertalker). It will take in a list (args), the function will then format it correctly so that the parameters are inputted correctly, i.e., args[0] -> self, args[1] -> from_name_or_id, args[2] -> to_name_or_id etc. 

#### Function Documentation -
load_transfer(...) documentation: Using the worker_info_api in [ot2_workcell_manager_client](ot2_workcell_manager) to obtain node information about the 2 OT2s doing the transfer and the arm that will do the transfer. It then creates a request using the service [LoadTransfer](rostalker2interface) and makes a request to the service /arm/<arm_id>/load_transfer, once it receives a response from the service it then decides what to do. A 10 (WAITING) signal will cause it to retry again after 6 seconds, an error will also cause it to retry with a wait of 6 seconds. If it is successful (0, SUCCESS) then it returns (0, SUCCESS) to whoever called it allowing the caller to do some work again. 

_load_transfer(...) documentation: Takes in list (called args) and just formats the input so that items in the list are mapped to parameters in the load_transfer(...) function call. It then returns whatever load_transfer returns. 

#### Services used -
/arm/<arm_id>/load_transfer     service type: [LoadTransfer](workcell_interfaces)  

#### APIs used - 
worker_info_api.py         API info: [ot2_workcell_manager_client](ot2_workcell_manager)   

## publish_arm_state_api.py
This API is used to publish the arm state to all the nodes involved and synchronized it across nodes so all state information is consistent across computers/robots. 

#### Functions 
1. update_arm_state(self, current_state) 
2. _update_arm_state(args) --> This is for retry support 

#### Function explanations - 

update_arm_state(self, current_state): This function will publish the state to the following topic /arm/<arm_id>/arm_state_update which will be received by the respective manager and the master of the system. In other words, this function will update the state of the robot and make it visible to the entire system and synchronize it so that all nodes that have that information have the same information about the state of the robot. It publishes to the topic using this msg type [ArmStateUpdate](workcell_interfaces). 

## armManager.py 
#### Purpose 
The purpose of the arm manager is to provide the state of the arm to other nodes in the system and to make the master aware that this arm exists in the system. Upon an error, it is the manager's job to remove itself from the master's records and to either stop actions or attempt to repair itself. It is also responsible for managing transfer requests. 

#### get_id_handler documentation 
Provide a way for the armTransferHandler to obtain the ID of the arm from the manager since the armTransferHanlder can't also register to the master along with the manager (multiple IDs).

#### completed_transfer_callback documentation
Upon completed transfer, the transfer handler will publish the information about the completed transfer to this callback function which will then store it in the completed_queue for OT2 nodes to determine if their transfer was completed 

#### get_next_transfer_handler docuemtnation
This handles get_next_transfer service requests by the transfer handler node. If there is a transfer waiting it sends that over to the transfer handler if not it tells the transfer handler to wait. 

#### load_transfer_handler documentation
This runs an algorithm to store requests from OT2 nodes that only now the starting location, destination, and item. This algorithm / handler will determine if the action has been completed already, if it needs to wait for the other side to be ready, or if the action can be completed and added to the queue. This also provides a way to block execution on OT2 nodes until the transfer is complete to prevent the arm from crashing into the OT2.

#### arm_state_update_callback documentation
This callback function stores state information provided by the transfer handler. 

#### Services provided -
/arm/<arm_name>/get_id     **service type:** [GetId](workcell_interfaces)  
/arm/<arm_id>/load_transfer   **service type:** [LoadTransfer](workcell_interfaces)  
/arm/<arm_id>/get_next_transfer  **service type:** [GetNextTransfer](workcell_interfaces)  

#### APIs used -
worker_info_api.py         **API info:** [ot2_workcell_manager_client](ot2_workcell_manager)  
register_api.py            **API info:** [ot2_workcell_manager_client](ot2_workcell_manager)  
retry_api.py               **API info:** [ot2_workcell_manager_client](ot2_workcell_manager)  

#### Services used - 
/register                  **service type:** [Register](workcell_interfaces)  
/deregister                **service type:** [Destroy](workcell_interfaces)  
/get_node_info             **service type:** [GetNodeInfo](workcell_interfaces)  

#### Topics used - 
/arm/<arm_id>/arm_state_update    **Message type:** [ArmStateUpdate](workcell_interfaces)  
/arm/<arm_id>/completed_transfer  **Message type:** [CompletedTransfer](workcell_interfaces)  

## armTransferHandler.py
#### Purpose 
Handle transfer service requests and keep the arm protocols separate from ROS 2 so that they require little to no change to be attached to the rostalker2 code. It will constantly poll the manager for work to do. 

#### get_next_transfer documentation
First will make a call to the service get_next_transfer, to see if there is a transfer waiting in the run_queue. If there isn't it waits, if there is it then begins getting transfer data, this requires special formatting as the input is also in a special format. It then retrieves node information from the master about the 2 involved in the transfer. It will then attempt to run a transfer script in a try block, if an error occurred it notifies the manager that something in the arm state is incorrect. If the transfer is completed it then publishes the completed transfer information to the completed transfers topic.

#### ROS2 Parameters - 
name                       **default value:** 'insert_arm_name_here'     **Usage:** To provide a name for the arm nodes 

#### Services provided -
None

#### Topics provided - 
/arm/<arm_id>/completed_transfer   **message type:** [CompletedTransfer](workcell_interfaces)  
/arm/<arm_id>/arm_state_update     **message type:** [ArmStateUpdate](workcell_interfaces)  

#### APIs used -
worker_info_api.py         **API info:** [ot2_workcell_manager_client](ot2_workcell_manager)  
retry_api.py               **API info:** [ot2_workcell_manager_client](ot2_workcell_manager)  
publish_arm_state_api.py   **API info:** [arm_client](arm_controller)  

#### Services used - 
/get_node_info             **service type:** [GetNodeInfo](workcell_interfaces)  
/arm/<arm_name>/get_id     **service type:** [GetId](workcell_interfaces)  
/arm/<arm_id/get_next_transfer **service type:** [GetNextTransfer](workcell_interfaces)  

