Glossary
========

**AD-SDL** builds on a science services framework, in the form of Globus Auth, Transfer, Search, Groups, and Flows, plus funcX function-as-a-service. 
These services provide a reliable, secure, and high-performance substrate to access and manage data and computing resources. Here we highlight
several of these services and describe how they are used to create Gladier deployments.

Locations
---------

**ANL** Argonne National Laboratory

**RPL**  Rapid Prototyping Lab in building 240 of ANL with workcell set up to run PCR and Color Picker Projects

**BIO** Bio building 446 of ANL with Bio Safety Level 2 facillity with workcell set up to run PCR with real DNA and bacteria growth curve experiments

Robots
------


**PF400**: 
The PF400 is the robot that sits central to the workcell in RPL, it is capable of moving wellplates between other instruments with micron level precision.
Module Link: `PF400`_.
.. _PF400: https://github.com/AD-SDL/pf400_module

**PlateCrane**:  
The Hudson PlateCrane Module is used to transport plates. There is one in RPL used for plate storage and one in bio used for instrument transfers. 

Module Link: `PlateCrane`_.

.. _PlateCrane: https://github.com/AD-SDL/platecrane_module


**Ur5**
The UR5 is the robot that sits central to the workcell in RPL, it is capable of moving wellplates between other instruments with micron level precision.

Find the Module Link Here: `PF400`_.

.. _PF400: https://github.com/AD-SDL/pf400_module

**MiR base**
The PF400 is the robot that sits central to the workcell in RPL, it is capable of moving wellplates between other instruments with micron level precision.

Find the Module Link Here: `PF400`_.

.. _PF400: https://github.com/AD-SDL/pf400_module

**Sciclops**
    
Instruments
-----------

**OT2**
**Sealer**
**Peeler**
**Hidex**


**WEI**

Workcell Execution Interface. Infrastructure for interpreting and running workflows on workcells. 

**Workcell**

Composition of one or more modules and the raw materials for running a workflow - a pedantic list of steps along with required resource in a workcell

**Workflow**

A pedantic list of steps along with required resource in a workcell

**Step**

An action on one module in a workflow consisting of instructions that the module can execute; the action is performed throughout the APIs that the module exposes

**Message**

A uniformly formatted command sent to and interpretable by a module in order to complete a step

**Action**

Part of a step, 1 to 1 relation, a specific function preformed by a module

**Protocol** 

A list of instructions interpretable by one instrument that will run all together as one action in a step

**Module** 

One or more instruments/robots, with associated clients and drivers, compute power, and cameras/sensors that exposes standardizes restricted APIs. 

**Instrument** 

A piece of hardware capable of executing actions or taking measurements

**Portal**

Globus portal, a website that can display data and archives experiment runs 

**Driver**

A software system that exposes the functionality of an instrument to the client

**Client**

API that standardizes an instruments communications and exposes them for use in a step

Experiment vs experiment (todo)

(capital experiment) 
**Experiment**

The code version of a lowercase e experiment

A script to call one or more workflow and manage the data they generate

(lowercase experiment) - a later problem

**Executor**

(WEI see above) generic interface for sending and receiving the messages associated with a step

(these are the options so far)

ROS 

TCP

REST

+other in future, maybe 

**Protopiler** 

Interprets high level protocol definition into machine executable code, currently part of OT-2 driver
**Resources**

disposable items required for in instrument to function properly. Example tape roll for peeler, 96-well plate for everything (labware), OT-2 pipette and tip boxes, etc

