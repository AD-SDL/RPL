Protocols
============================

## Protocol definition

A protocol file gives the device-specific instructions to be executed on a specific piece of hardware to implement an intended action. For example, [ot2_pcr_config.yaml](https://github.com/AD-SDL/rpl_workcell/blob/main/pcr_workcell/protocol_files/ot2_pcr_config.yaml) gives instructions for an OpenTrons OT2. A protocol file specifies a list of **equipment** within the hardware component; a sequence of **commands** to be executed on the equipment; and some describptive **metadata**. For example, the following shows the contents of [combined_protocol.yaml](https://github.com/AD-SDL/rpl_workcell/blob/main/color_picker/protocol_files/combined_protocol.yaml), which comprise the equipment section, three commands, and the metadata section. 

Strings of the form *payload.VARIABLE* (e.g., `payload.destination_wells`) refer to arguments passed to the protocol.

The "location" argument here is OT2-specific: it indicates one of 11 plate locations, numbered 1..11:

<img src="assets/DeckMapEmpty.jpg"  width="200">

An "alias" argument defines a string that can be used to refer to a position later in the specifrication: e.g., the fourth line in the YAML below specifies that location "7" can be referred to as "source". 

The wells within a plate are referred to via their column and row, e.g., A1. 

The following specification describes an OT2 with the following components:
* In location 7: A 6-well rack of 50 ml tubes. (These are used to contain the different colors that are to be mixed, in wells A1, A2, and A3.
* In each of locations 8 and 9: A 96-well rack of 300 ul wells.

```
equipment:
  - name: opentrons_6_tuberack_nest_50ml_conical
    location: "7"
    alias: source  # Define "source" as an alias for location 7
  - name: opentrons_96_tiprack_300ul
    location: "8"
  - name: opentrons_96_tiprack_300ul
    location: "9"

commands:
  - name: Mix Color 1                       # Transfer fluid: A1 -> specified locations 
    source: source:A1
    destination: payload.destination_wells  # Destination wells for transfers (argument)
    volume: payload.red_volumes             # Volumes to be transferred  (argument)
    dispense_clearance: 2
    aspirate_clearance: 1
    drop_tip: False

  - name: Mix color 2
    source: source:A2
    destination: payload.destination_wells
    volume: payload.green_volumes
    dispense_clearance: 2
    aspirate_clearance: 1
    drop_tip: False    
  
  - name: Mix color 3
    source: source:A3
    destination: payload.destination_wells
    volume: payload.blue_volumes
    dispense_clearance: 2
    aspirate_clearance: 1
    mix_cycles: 3
    mix_volume: 100
    drop_tip: False

metadata:
  protocolName: Color Mixing all
  author: Kyle khippe@anl.gov
  description: Mixing all colors
  apiLevel: "2.12"
```