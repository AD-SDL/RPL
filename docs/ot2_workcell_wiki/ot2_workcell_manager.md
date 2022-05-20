# Purpose
The purpose behind the ot2_workcell_manager is to provide a manager who keeps track of all the workers, it also is responsible for housing services to send files to other workers and run services on other workers. The manager is also responsible for adding to the queues of the worker nodes. 

# Files
* **ot2_workcell_manager/**
	* **ot2_workcell_manager/**
		* master.py (Controls the state of the system)  
		* state_reset_handler.py (Allows for human intervention into the error system) 
* **ot2_workcell_manager_client/**
	* **ot2_workcell_manager_client/**
		* register_api.py (registration to the master api)
		* retry_api.py (api to allow users to run a function in an isolated manner)
		* worker_info_api.py (api to allow workers to retrieve other worker info from the master)

# Dependencies
This section goes over the dependencies of the packages.
## ot2_workcell_manager
Dependencies:
1. [ot2_client](ot2_controller)
2. [arm_client](arm_controller)
3. [ot2_workcell_manager_client](ot2_workcell_manager)
4. [workcell_interfaces](workcell_interfaces)

## ot2_workcell_manager_client
Dependencies:
1. [workcell_interfaces](workcell_interfaces)

# ot2_workcell_manager bringup 
1. source ~/ot2_ws/install/setup.bash  
2. ros2 run ot2_workcell_manager master

# state_reset_handler bringup
1. source ~/ot2_ws/install/setup.bash  
2. ros2 run ot2_workcell_manager state_reset_handler

# File Documentation
This section discusses the various files in the packages. 

## master.py
This file contains the main ot2_workcell_manager class and houses all the node information (state, name, id, type). It is also responsible for adding to the queues of the worker nodes, this includes the OT2s and the arm. It handles the registration deregistration services, the node info requests, and contains the files to send over to other nodes. 

#### Services Provided -
1. /register **service type:** [Register](workcell_interfaces) 
2. /destroy **service type:** [Destory](workcell_interfaces)
3. /get_node_info **service type:** [GetNodeInfo](workcell_interfaces)
4. /get_node_list **service type:** [GetNodeList](workcell_interfaces)
5. /send_files **service type:** [SendFiles](workcell_interfaces)

#### APIs used -
1. retry_api.py **API info:** [retry_api](ot2_workcell_manager)
2. transfer_api.py **API info:** [transfer_api](arm_controller)

#### register_handler
This handler will take a request which contains a type and name. The type is then checked to make sure it is an acceptable name. The node is then given a unique id and the information is stored in the nodes_list. 

#### destroy_handler
This handler will take a request which contains a new or id and removes it from the nodes_list. This prevents further actions from being done on a bad node. 

#### get_node_info
This handler will return the entry in nodes_list for a given node (name or id). 

#### get_node_list
This handler will return the entire nodes_list to the caller. 

#### send_files
Client that sends string of file names listed in setup file to the ot2_controller node over the SendFiles topic.

## state_reset_handler
This file provides a way to reset states of specific nodes, this allows human intervention to manual fix errors in the arm or OT2 and then be able to resume operation by using this node

#### Topics used - 
1. /arm/<arm_id>/arm_state_reset **topic info:** [ArmReset](workcell_interfaces)
2. /OT_2/<ot2_id>/ot2_state_reset **topic info:** [OT2Reset](workcell_interfaces)

#### APIs used - 
1. worker_info_api.py **API info:** [worker_info_api](ot2_workcell_manager)

#### node_state_reset
This function will constantly be run until the user types in 'Q'. To start a reset type in 'Y' and enter the nodes name, it will then search for that node in the master. Once found it will then ask for confirmation (Y/N) to proceed with the state reset. At any point, if the wrong is entered the process is restarted. All inputs are case-sensitive. It is best to not reset the state unless the system is in an error state. Doing a state reset when the node is in a READY or BUSY state could cause an unstable state of the machine. 

## register_api.py
This houses the register functions. 

#### register - 
This allows a node to register with the master. There is also a function to allow the ability to run this function in the retry api.

#### deregister - 
This allows a node to deregister with the master. There is also a function to allow the ability to run this function in the retry api.

#### get_id_name
Function to retrieve id and name from a node manager. There is also a function to allow the ability to run this function in the retry API.

## retry_api.py
This provides a way of running a function in an isolated manner. Errors can be caught and the function can be retried with debug output. This provides an easy was to retry functions, add a timeout, catch errors, and provide output to logs. 

#### retry function
Takes in the following parameters (node, function, retry times, timeout time in seconds, args). 

## worker_info_api.py
Provides a way to retrieve node information from the master. 

#### get_node_info
Function to get the entry of node from the master. 

#### get_node_list
Function to get the full node list from the master.  
