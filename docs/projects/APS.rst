Robotic Pendant Drop: AI-executable Synchrotron Coherent X-ray Probe on Container-less Complex Fluid
====================================================================================================

A complex fluid refers to a material with a mixture of two or more phases that is microscopically stochastic and macroscopically stable, e.g. milk, toothpaste, hair gel, etc. 
Synchrotron coherent x- ray beamlines provide unique insight into the structure formation and dynamics evolution in complex fluid because of the laser-like beam quality from magnetic undulator sources and the high-penetration power of sub-nm x-rays. 
To this date, all sample changes at coherent synchrotron x-ray scattering beamlines in the world are performed manually, with a rigid search process to assure the hutch is evacuated prior to commencing the experiment. 
Although container-less liquid (e.g. acoustic levitation or pendant drop) can enable automated and high-throughput sample exchange, the oscillation of the liquid drop at μm-level could contaminate the coherent x-ray scattering results, which are acquired using micro-focused x-ray beam commensurate with the sample oscillation.


In this work, we demonstrate that a pendant drop shielded from ambient air turbulence yields results quantitatively consistent with samples in generic liquid containers (e.g. thin-walled quartz capillaries), validating the use of pendant drop for synchrotron coherent x-ray scattering experiments. 
The pendant drop can be aspirated by an electronic pipette and withdrawn into a pipette tip, and the electronic pipette can be mounted on a robotic arm to access waste sample pits and reservoirs of stock samples. 
The robotic pendant drop features high precision and high repeatability in the preparation of liquid samples with a tailored composition profile. 
In addition, the entire life cycle of the complex liquid sample, i.e., preparation, characterization, and disposal, can be fully automated without human intervention. 
To improve robotic integration at synchrotron beamlines, our method utilizes a single python script that interacts with backends of open-source libraries specializing in both the beamline control (Experimental Physics and Industrial Control System, EPICS) and robots (URx library from Universal Robots). 
Leveraging the Python ecosystem at colossal scientific user facilities allows for AI toolkits to be adapted within unified Python interface to achieve end-to-end AI-driven experiments, providing the foundation for autonomous, self-driving material design with a collaborative development platform.