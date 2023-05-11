## Workcell definition

A workcell definition is a YAML file (e.g., [pcr_workcell.yaml](https://github.com/AD-SDL/rpl_workcell/blob/main/pcr_workcell/pcr_workcell.yaml)) comprising two sections, *config* and *modules*:

The **config** section defines various infrastructure services that may be used elsewhere in the workcell. For example, here is the config from the example just listed.

```
  ros_namespace: rpl_workcell                                 # ROS variable namespace name
  funcx_local_ep: "299edea0-db9a-4693-84ba-babfa655b1be"      # UUID for funcX endpoint used for local computations
  globus_local_ep: ""                                         # 
  globus_search_index: "aefcecc6-e554-4f8c-a25b-147f23091944" # UUID for the Globus Search instance
  globus_portal_ep: "bb8d048a-2cad-4029-a9c7-671ec5d1f84d"    # UUID for the portal to which data may be published
  globus_group: "dda56f31-53d1-11ed-bd8b-0db7472df7d6"        # 
```

The **modules** section lists the *modules* that are included in the workcell. In the example just listed, there are 12 in total: 
* a [pf400 sample handler](https://preciseautomation.com/SampleHandler.html) (**pf400**) and two associated cameras, **pf400_camera_right** and **pf400_camera_left**; 
* a [SciClops plate handler](https://hudsonrobotics.com/microplate-handling-2/platecrane-sciclops-3/) (**sciclops**)
* a [A4S](https://www.azenta.com/products/automated-roll-heat-sealer-formerly-a4s) (**sealer**) and a [Brooks XPeel](https://www.azenta.com/products/automated-plate-seal-remover-formerly-xpeel) (**peeler**), with an associated camera, **sp_module_camera**
* three [OpenTrons OT2](https://opentrons.com/products/robots/ot-2/) liquid handlers, **ot2_pcr_alpha**, **ot2_pcr_beta**, and **ot2_cp_gamma**;
* a [Biometra thermal cycler](https://www.analytik-jena.com/products/life-science/pcr-qpcr-thermal-cycler/thermal-cycler-pcr/biometra-trio-series/) (**biometra**)
* another camera module, **camera_module**
           
For example, this module specification included in [pcr_workcell.yaml](https://github.com/AD-SDL/rpl_workcell/blob/main/pcr_workcell/pcr_workcell.yaml) described the Sealer module:

```
  - name: sealer                     # A name used for the module in the workflow: its "alias"
    type: wei_ros_node               # Indicates that module uses ROS2
    model: sealer                    # Not used at present
    config:
      ros_node: "/std_ns/SealerNode" # ROS2 network name (in name space)
    positions:                       # One or more spatial locations, with name 
      default: [205.128, -2.814, 264.373, 365.863, 79.144, 411.553]
```

The positions here are specific to the PF400: they give joint angles. ???Why does the Sealer have PF400 angles???

For other modules, a module specification could include things like protocol and IP port.