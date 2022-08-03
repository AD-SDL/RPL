---
layout: project
title:  "API Development and Integration"
image: "rpl.jpg"  
teaser: "A collaborative space for prototyping robotic instrument integrations before deployment into production."
featured: true
description: "The Rapid Prototyping Laboratory (RPL) provides a prototyping space for Argonne's Autonomous Discovery effort and serves as a hub for students and cross-lab collaboration." 


---

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
- link: <https://www.azenta.com/automated-plate-sealer>

Azenta Plate Seal Remover

- model number: TODO
- <https://www.azenta.com/products/automated-plate-seal-remover-formerly-xpeel>

Related GitHub repo:
<https://github.com/AD-SDL/azenta_driver>

**Hudson Plate Crane**

On our current production-ready automated robotic platform, we make use of a Hudson PlateCrane EX Robotic Arm Microplate Handler. The use of this plate crane is greatly limited by the vendor provided control software. Students on this project will develop a python API capable of controlling Hudson's next generation microplate handler, the Hudson SciClops, though direct USB communication. This will help to enable flexible, open-source, and fully automated biology workflows going forward.

Instrument Details:

Hudson SciClops Microplate Handler

- model number: TODO
- link: <https://hudsonrobotics.com/microplate-handling-2/platecrane-sciclops-3/>

Related GitHub repo:
<https://github.com/AD-SDL/hudson_driver>

**Thermocycler**

Our production-ready automated robotic platform does not contain a thermocycler which limits the platform's capabilities with biological workflows. A thermocycler is needed to enable fully automated DNA Assembly, a workflow that Argonne is very interested in implementing. Students on this project will create a python API and ROS2 layer to interface with Analytic Jena Biometra TRobot IIs. This will enable the use of this thermocycler on our future fully open-source robotic experimentation platforms.

Instrument Details:

Analytik Jena Biometra TRobot II

- model number: TODO
- link: <https://www.analytik-jena.com/products/life-science/pcr-qpcr-thermal-cycler/thermal-cycler-pcr/biometra-trobot-ii-series/>

Related GitHub Repo:
<https://github.com/AD-SDL/biometra_driver>
