# Purpose
The purpose behind the ot2_controller / ot2_client packages (ot2_controller, protocol_manager, load_run_api, publish_ot2_state_api) is to provide a way to communicate with the ot2 through a ROS 2 network and easily attach any arm protocols with little to no modification. It is also to provide a clean and easy-to-use API for other packages to easily obtain information about the ot2, request transfers, and obtain the current state of the ot2.

# Driver Creation Documentation 
**Location:** Must be in a package named `ot2_driver_pkg` and all functions must be in the file `ot2_driver.py` and packages must follow ROS2 format. 
## Function Description 
**load_protocol(<protocol_path (path to the protocol we want to load)>, <robot_id (ROS layer's ID for the robot)>)** - Loads a protocol to the ot2_driver to be run on the internal RPI4 (inside ot2). This makes it so the ROS layer doesn't need to know how to get protocols to run on the OT2 it only knows the high level view of run on robot nothing more.  
**run_protocol( <protocol_id (id of the protocol)>, <username (for the database will be moved out)>, <ip (for the database)>, <port (for the database)>)** - this will run a given protocol_id on the ot2. 

# Files
**ot2_controller/**  
&nbsp;&nbsp;	**ot2_controller/**  
&nbsp;&nbsp;&nbsp;&nbsp;		ot2_controller.py (Controls the OT2 )  
&nbsp;&nbsp;&nbsp;&nbsp;		protocol_manager.py (removes items from the queue in manager)  

**ot2_client/**  
&nbsp;&nbsp;	**ot2_client/**  
&nbsp;&nbsp;&nbsp;&nbsp;	load_run_api.py (TODO)  
&nbsp;&nbsp;&nbsp;&nbsp;	publish_ot2_state_api.py (api to publish the state of the ot2 to manager)  

# Dependencies 
This section discusses the package dependencies. 

## ot2_controller 
dependencies are: 
1. [workcell_interfaces](workcell_interfaces)
2. [ot2_workcell_manager_client](ot2_workcell_manager)
3. [arm_client](arm_controller)
4. [ot2_client](ot2_controller)

## ot2_client
dependencies are: 
1. [workcell_interfaces](workcell_interfaces)
2. [ot2_workcell_manager_client](ot2_workcell_manager)

# OT2 Bring Up (Launch ot2)
**launch bob** (For testing): 
1. source ~/ot2_ws/install/setup.bash
2. ros2 launch ot2_controller ot2_bob_bringup.launch.py

**launch alex** (For testing): 
1. source ~/ot2_ws/install/setup.bash
2. ros2 launch ot2_controller ot2_alex_bringup.launch.py

## Note! The below might not be up to date! 
# File Documentation 
This section discusses the various APIs available to ot2_controller. 

## load_run_api.py
This API houses all the old load and run functions, these currently have no use and are just kept for storage purposes please refer to the functions in the ot2_controller and protocol_manager for loading and running files 

#### Functions -
1. run (_run for retry support)
2. load (_load for retry support) 
3. load_and_run 

## publish_ot2_state_api.py
This function houses the ability to publish the ot2 state to the master and the manager of the ot2. 

#### Functions - 
1. update_ot2_state(self, current_state) 
2. _update_ot2_state(args) --> This is for retry support 

#### Function explanations - 

update_ot2_state(self, current_state): This function will publish the state to the following topic /OT_2/<ot2_id>/ot2_state_update which will be received by the respective manager and the master of the system. In other words, this function will update the state of the robot and make it visible to the entire system and synchronize it so that all nodes that have that information have the same information about the state of the robot. It publishes to the topic using this msg type [OT2StateUpdate](workcell_interfaces). 

## ot2_controller.py
This acts as the manager for an OT-2 and handles communication with the master and the queue.

#### Functions -
1. load_scripts_handler
2. receive_files_handler
3. state_reset_callback
4. ot2_state_update_callback
5. get_id_handler
6. protocol_handler

#### Function explanations -

#### protocol_handler documentation 
This is to handle service calls to the service /OT_2/<ot2_id>/protocol which is used by the protocol_manager node to retrieve the next protocol.   

The first thing when running this function is it verifies the state of the robot. It ensures that the state of the robot is in 'READY' or else it returns a WAITING response to whoever called the service. It then accesses the work_list. If the worklist is empty it returns a WAITING response to the caller, if not it pops out the next batch of jobs and puts it in temp_list. If the state somehow changed mid execution, before we run anything we then check the state again and ensure that the system is in a correct state. A response is then created using the service [Protocol](workcell_interfaces0. The just returns the file name of the next protocol to be run in the temp_list batch and sends it over to the caller which is most likely the protocol_manager node. 

#### get_id_handler 
This is used by the protocol_manager to retrieve the id of the group of nodes for that specific OT_2. 

#### ot2_state_update_callback 
This is used to update the state of the ot2_controller node 

#### state_reset_callback
This is used by humans to intervene with the state and reset robots to continue operation after some repairs 

#### recieve_files_handler
This handles the service call /OT_2/<ot2_id>/send_files

Retrieves request information from the service type [SendFiles](workcell_interfaces) which contains the batch of files to be added to the queues. It then adds the batch of files to the work_list and increases the work_index. Depending on how this goes the service response is either an ERROR status or SUCCESS status.

#### load_scripts_handler
This handles the service call /OT_2/<ot2_id>/send_scripts

Retrieves request information from the service type [SendScripts](workcell_interfaces) which contains a single file and its contents. It will check to see if a file of that name already exists and, depending on whether the "replace" request is true or false, overwrite that existing file. If the file does not exist yet, it will create it and write the contents within it. The service response is a status will either be SUCCESS or ERROR.

## protocol_manager.py 
The purpose of protocol_manager.py is to get items from the manager of the OT_2 and load/send the files over to the actually OT_2 to run, it is also responsible for letting the manager and master know the state of the running machine. 

#### Functions -
1. get_next_protocol
2. state_reset_callback
3. load_and_run
4. set_state
5. run
6. transfer

#### Function explanations -

#### transfer 
This is a helper function to make a call to the [transfer_api](arm_controller) and initiate a transfer. 

#### run 
This just starts spinning and continuously calls get_next_protocol every 3 seconds while the node is ok(). 

#### set_state
This a helper function to set the state and synchronize the state across the different nodes involved. See publish_ot2_state_api.py 

#### load_and_run
This function will first ensure the protocol exists on the system. It will then import the module into the ROS 2 infrastructure and then execute the function work() from that file. Notice that the function it runs is **work()** with no parameters, it doesn't make a call to any other function. Notice: This will change in future versions. 

#### state_reset_callback
This is used to reset the state of the robot after an error occurred

#### get_next_protocol
This makes a service call using the service type [Protocol](workcell_interfaces) to the service /OT_2/<ot2_id>/protocol to retrieve the next protocol. After receiving the next protocol it then saves the name and updates the robot state to busy. It then attempts to run the protocol by running the load_and_run function. If that was successful the state becomes READY and it retrieves another protocol in 3 seconds. If an error occurred the robot state is set to ERROR which blocks further execution until human intervention fixes the problem using the [state_reset_handler node](ot2_workcell_manager).