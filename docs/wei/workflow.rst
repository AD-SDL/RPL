## Workflow definition

This is specified by a YAML file that defines the sequence of actions that will be executed in order on the hardware. E.g., see [this example](https://github.com/AD-SDL/rpl_workcell/blob/main/color_picker/workflows/cp_wf_mixcolor.yaml), shown also in the following, and comprising four sections:
* **metadata**: Descriptive metadata for the workflow
* **workcell**: The location of the workcell for which the workflow is designed
* **modules**: A list of the modules included in the workcell--four in this case.
* **flowdef**: A list of steps, each with a name, module, command, and arguments.


```
metadata:
  name: PCR - Workflow
  author: Casey Stone, Rafael Vescovi
  info: Initial PCR workflow for RPL workcell
  version: 0.1

workcell: /home/rpl/workspace/rpl_workcell/pcr_workcell/pcr_workcell.yaml

modules:
  - name: ot2_cp_gamma
  - name: pf400
  - name: camera

flowdef:
  - name: Move from Camera Module to OT2
    module: pf400
    command: transfer
    args:
      source: camera_module.positions.plate_station
      target: ot2_cp_gamma.positions.deck2
      source_plate_rotation: narrow
      target_plate_rotation: wide
    comment: Place plate in ot2

  - name: Mix all colors
    module: ot2_cp_gamma
    command: run_protocol
    args:
      config_path:  /home/rpl/workspace/rpl_workcell/color_picker/protocol_files/combined_protocol.yaml
      red_volumes: payload.red_volumes
      green_volumes: payload.green_volumes
      blue_volumes: payload.blue_volumes
      destination_wells: payload.destination_wells
      use_existing_resources: payload.use_existing_resources
    comment: Mix the red portions according to input data

  - name: Move to Picture
    module: pf400
    command: transfer
    args:
      source: ot2_cp_gamma.positions.deck2
      target: camera_module.positions.plate_station
      source_plate_rotation: wide
      target_plate_rotation: narrow

  - name: Take Picture
    module: camera_module
    command: take_picture
    args:
      save_location: local_run_results
      file_name: "final_image.jpg"
```


This workflow uses three of 12 modules defined in the workcell definition earlier, **pf400**, **ot2_pcr_gamma**, and **camera_module**.
It comprises four steps:
* Transfer a plate from `camera_module.positions.plate_station` to `ot2_cp_gamma.positions.deck2`, while rotating the plate 90 degrees
* Run the "protocol" defined by the file [ot2_pcr_config.yaml](https://github.com/AD-SDL/rpl_workcell/blob/main/color_picker/protocol_files/combined_protocol.yaml). 
This file specifies a sequence of steps to be performed on the hardware.
* Transfer the plate to the camera
* Take a picture of the plate

> While a workflow and a protocol both specify a sequence of actions to be performed, they are quite different in role and syntax. A **workflow** uses a hardware-independent notation to specify actions to perform on one or more modules (e.g., action A1 on module M1, action A2 on module M2); a **protocol** uses a hardware-specific notation to specify steps to be performed on a single module (e.g., OT2). Why *workflow* and *protocol*? Perhaps because this technology was developed by a partnership of computer scientists ("module", "workflow") and biologists ("protocol") :grinning:
