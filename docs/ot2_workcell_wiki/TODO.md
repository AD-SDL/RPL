# TODO's for the ot2_workcell repo
Various changes that need to happen. 

## OT2 Driver Changes 
1. `ot2_client` and `ot2_controller` can be moved into the `ot2_driver_pkg` repo and out of the current repo. 
2. Packages inside `ot2_driver_pkg` need to be moved into one central package instead of split into so many different package names. In the future those will cause conflicts with other packages due to naming clashes. 
3. `ot2_driver_pkg` `setup.py` file can be nested to allow for less restrictive names. 
4. Custom service and message types need to be moved out of the `ot2_workcell` package and into there own package and listed as a dependency for `ot2_driver_pkg`

## Arm Driver Changes 
1. `arm_controller` and `arm_client` need to be moved to `workcell-manager` repo. Since they are generalized they would be misplaced if placed in the `PF400_cobot` repo. 
2. Cleanup of the `PF400_cobot` repo, this entails the `resources/` folder and moving files into one central package instead of distributed among so many packages (can cause naming clashes). 
3. `workcell_interaces` needs to be moved to its own repo (duplicate of OT2 Driver Changes 4) and marked as a dependency for this package. 

## Scheduler Driver Changes 
1. `scheduler_controller` and `scheduler_client` need to be moved to the `workcell-manager` package. 
2. The files for deadlock detection and testing in `scheduler_client` should be moved into the scheduler_controller package as they aren't consistent with what files are in the client package. (Need to update setup.py to do this change) (Note: if it is possible to move this to the arm packages it would make sense to do so. **But** currently it is very abstract and would be better placed in the `scheduler_controller` package).
3. `workcell_interaces` needs to be moved to its own repo (duplicate of OT2 Driver Changes 4) and marked as a dependency for this package.
4. **Future Change:** we need to make it easier for the user to program workflow files (transfer are unreadable, json files get too complicated), instead of reinventing the wheel using Amazon's step-functions might be an option. 
5. **Future Changes:** make it easier to shutdown all the robots with a basic python script that basically shuts down all the various nodes on the system. 

## ot2_workcell repo changes 
1. All of the above (moving things out of this repo) 
2. Updating the install README in the repo to implement the above changes 

## Other Changes 
1. None currently 

 
