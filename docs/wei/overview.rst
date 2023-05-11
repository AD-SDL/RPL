Workflow Execution Interface
============================

WEI (Workflow Execution Interface) is a simple message parser.

# Background on Workcells, Carts, Modules, and Workflows

We define conventional hardware and software configurations for robotic equipment and control software in order to simplify the assembly, modification, and scaling of experimental systems. The following figure shows our hardware conventions:
* A **cart** is a cart with zero or more modules 
* A **module** is an hardware component with a name, type, position, etc. (e.g., Pealer, Sealer, OT2 liquid handling robot, plate handler, plate mover, camera)
* A **workcell**, as show on the left of the image, is formed from multiple (8 in the photo on the left) carts that typically hold multiple modules (12 in the example, as described below).
* Multiple workcells and other components can be linked via mobile robots

![Image of a workcell with eight carts, connected via mobile robots to other workcells; on the far right, a workflow definition.](assets/AD_Fig.jpg)

A **workcell definition** (a YAML file, see below) defines the modules that comprise a workcell, and associated static infrastructure that are to be used by the workflow.

The software associated with a workflow is then defined by three types of files:
* A **driver program**, in Python, sets up to call one or more workflows
* A **workflow definition**, in YAML, define a set of **actions** to be executed, in order, on one or more of the modules in the workcell
* A **protocol definition**, in YAML, defines a set of steps to be performed, in order, on a specified OpenTrons OT2

The figure illustrates the three components for a simple "Color Picker" application that we use to illustrate the use of the technology. 

![Software involved in Color Picker.](assets/ColorPicker.jpg)


.. toctree::
   :maxdepth: 2

   workcell
   workflow
   protocols
   experiment