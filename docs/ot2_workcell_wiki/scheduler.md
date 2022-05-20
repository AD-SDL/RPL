# Purpose
The purpose of the scheduler is to schedule blocks submitted to ot2_workcell and schedule on any available resources without the user having to manually specify how jobs run. It is all done automatically with the scheduler. 

# Driver Creation Documentation
TODO, not yet a driver very deeply tangled with ROS layer. 

# Scheduler Information 
The scheduler we currently have is a batch scheduler running a first come first serve (FCFS) model. The first available OT2 is assigned the next protocol in the queue of the batch scheduler. 

# Files 
**scheduler_controller/**  
**scheduler_client/** 

# Deadlock detection 
Due to arm transfers causing deadlocking problems there are various deadlock safety checks in place to prevent the user from submitting errored workflow files from shutting down the system. Deadlock detection functions are located in `scheduler_client/transfer_deadlock_detection.py`. 