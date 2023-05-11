## Command file

A Python program defines the process required to run an experiment. E.g., see [color_picker_loop.py](https://github.com/AD-SDL/rpl_workcell/blob/main/color_picker/color_picker_loop.py) for a color picker program, which calls three workflows: 
* First, if needed, `cp_wf_newplate.yaml`
* Then, the workflow given above, `cp_wf_mixcolor.yaml`
* Finally, as needed, `cp_wf_trashplate.yaml`
