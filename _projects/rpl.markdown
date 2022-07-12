---
layout: project
title:  "Rapid Prototyping Laboratory (RPL)"
image: "funcx.png"  
teaser: "A collaborative space for prototyping robotic instrument integrations before deployment into production."
featured: false
description: "The Rapid Prototyping Laboratory (RPL) provides a prototyping space for Argonne's Autonomous Discovery effort and serves as a hub for students and cross-lab collaboration." 


---

The integration of robotic experimentation with AI/ML optimization for the purposes of autonomous discovery requires an immense troubleshooting effort early on. This troubleshooting often occurs at the expense of production productivity. Argonne’s Rapid Prototyping Laboratory aims to reduce this burden on productivity by providing a prototyping space for Argonne’s autonomous discovery effort and serving as a hub for cross-lab collaboration. 

Student daily logs: https://github.com/AD-SDL/rpl-summer-2022

## RPL Projects: 

### API Development and Integration

Mentors: 
</br>Rafael Vescovi
</br>Doga Ozgulbas
</br>Casey Stone

Students: 
</br>Sanjiv Parthasarathy
</br>Noah Grom

**Plate Sealer/Plate Peeler**

Many molecular biology reactions are carried out in 96 or 386-well plates and require the use of a thermocycler or incubator. To prevent the evaporation of reaction contents under the heat of those instruments, a seal must be placed on the labware before heating and removed after heating. Currently, our robotic platforms lack this capability which limits the breadth of biological protocols we are able to perform. 

We recently purchased two instruments for the RPL, an Azenta plate sealer and plate peeler. Instrument details are provided below. Students on this project will develop a python API to allow fully open-source and automated control of both instruments. 

Instrument Details: 

Azenta a4S Automated Plate Heat Sealer
- model number: TODO
- link: https://www.azenta.com/automated-plate-sealer

Azenta Plate Seal Remover 
- model number: 
- https://www.azenta.com/products/automated-plate-seal-remover-formerly-xpeel

Related GitHub repo: 
https://github.com/AD-SDL/azenta_driver

**Hudson Plate Crane**

On our current production-ready automated robotic platform, we make use of a Hudson PlateCrane EX Robotic Arm Microplate Handler. The use of this plate crane is greatly limited by the vendor provided control software. Students on this project will develop a python API capable of controlling Hudson's next generation microplate handler, the Hudson SciClops, though direct USB communication. This will help to enable flexible, open-source, and fully automated biology workflows going forward. 

Instrument Details: 

Hudson SciClops Microplate Handler
- model number: TODO
- link: https://hudsonrobotics.com/microplate-handling-2/platecrane-sciclops-3/

Related GitHub repo: 
https://github.com/AD-SDL/hudson_driver

**Thermocycler**

Our production-ready automated robotic platform does not contain a thermocycler which limits the platform's capabilities with biological workflows. A thermocycler is needed to enable fully automated DNA Assembly, a workflow that Argonne is very interested in implementing. Students on this project will create a python API and ROS2 layer to interface with Analytic Jena Biometra TRobot IIs. This will enable the use of this thermocycler on our future fully open-source robotic experimentation platforms. 

Instrument Details: 

Analytik Jena Biometra TRobot II
- model number: TODO
- link: https://www.analytik-jena.com/products/life-science/pcr-qpcr-thermal-cycler/thermal-cycler-pcr/biometra-trobot-ii-series/

Related GitHub Repo: 
https://github.com/AD-SDL/biometra_driver

### Modular Robotics for Science

Scientific workflows often rely on domain specific instruments. This project aims to engineer ""modules"" of commonly required instruments to assemble robotic experimentation platforms for certain scientific workflows. This project will encompass both the hardware and software aspects of developing new modules. 

At first approach, the modules will replace already existing instruments to minimize the utilization gap. Furthermore, new instruments will be introduced and new scientific workflows purely based on the modules. The student will also be linked with domain scientists to bridge the gap between development and real-life utilization.

Mentors: 
</br>Rafael Vescovi
</br>Doga Ozgulbas
</br>Mark Herald

Students: 
</br>Sanjiv Parthasarathy
</br>Kendrick Xie
</br>Eric Codrea
</br>Noah Grom

### Automation of OT-2 Calibration

Biological protocols can be run via a python API on the Opentrons OT-2 liquid handler, but the calibration of the OT-2 is performed in an interactive session, preventing the development of fully autonomous workflows. This project aims to develop an automated calibration method using microswitches and an Arduino microcontroller. The Python-based utility will calibrate the pipette followed by the calibration of the deck.

Mentors: 
</br>Gyorgy Babnigg
</br>Casey Stone
</br>Ryan Lewis

Students: 
</br>Miriam Stevens (summer 2021)

### ROS Package Development for Precise Automation PF400

Mentors: 
</br>Doga Ozgulbas
</br>Rafael Vescovi

Students: 
</br>Sanjiv Parthasarathy
</br>Eric Cordea
</br>Kendrick Xie

### Pyhamilton Protocol Implementation on Hudson Robotic Platform

In a recent paper entitled Flexible open-source automation for robotic engineering (Chroy et al. 2021), a new software package named Pyhamilton was presented which allows the user to program the actions of Hamilton STAR and STARlet liquid handling robots using standard Python. The capabilities of Pyhamilton were demonstrated by preforming several biological experiments including the use of a feedback loop to maintain culture turbidostats and a high-throughput perturbation analysis of metabolites.

For this project, we will reproduce one of the biological experiments presented in this paper using the Python interface that has been developed for the Hudson SOLO liquid handler and Hudson SoftLinx integration system. We aim to prove that our completely open-source Python API can execute the same biological experiments as Pyhamilton with similar results. Students on this project will also contribute to the growing library of biological protocols written for our Hudson robotic experimentation platform.

Link to Pyhamilton paper: 
https://pubmed.ncbi.nlm.nih.gov/33764680/

Mentors: 
</br>Casey Stone 
</br>Abraham Stroka 
</br>Priyanka Setty

Students: 
</br>Gillian Camacho
</br>Arleen Hidalgo
</br>Halona Dontes 

### Vision System Integrated Debugger

This project aims to enable computer vision capabilities on a mobile robot in such a way that decisions can be made local to the robot in real time based on video input. This includes design and initial development of a vision API.  This could include adding vision to UR5e arm so that QR-type tags could (1) identify fiducial positions to provide a coordinate system transformation to enable accurate interactions with mobile arm and things on static tables, and (2) identify things of interest called out by name in protocol: “beaker 7”, “start button”, “trash bin”

Related projects include the development of vision packages for real-time coordination of mobility (based on MiR250 cameras); Dexterity (based on UR5e movements) and experiment control based on experiment specific tagging. 

Mentors: 
</br>Rory Butler

Students
</br>Amaan Khan 
</br>Halona Dantes
</br>Saaya Patel

### DNA Assembly Protocol Development

DNA Assembly is the method of physically linking together fragments of DNA, in an end-to-end fashion, to achieve a desired, higher-order assembly prior to joining to a vector.  This is one of the most important protocols in molecular biology and will be a vital capability of our larger autonomous laboratory in the future. There are also several existing projects at Argonne that would benefit greatly from this AI enabled DNA Assembly protocol. For now, this protocol will be developed on the Hudson robotic platform in building 446. In the future, we would like to move this protocol to a more open-source robotic platform like the ones that are being developed in the Rapid Prototyping Lab in building 240. 

Mentors: 
</br>Tom Brettin
</br>Casey Stone
</br>Abraham Stroka

Students: 
</br>Priyanka Setty









