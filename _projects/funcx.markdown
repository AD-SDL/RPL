---
layout: project
title:  "funcX"
image: "funcx-logo.png"
teaser: "funcX is a Function as a Service platform for scientific computing."
featured: true
description: "funcX is a Function as a Service (FaaS) platform for science. It is designed to be applied to existing cyberinfrastructures to provide scalable, secure, and on-demand execution of short duration scientific functions."
---

Increasing data volumes and velocities are driving exciting new methods across the sciences in which data analytics and 
machine learning are increasingly intertwined with research. These new methods require new approaches for scientific 
computing in which computation is mobile, so that, for example, it can occur near data, be triggered by events (e.g., arrival of 
new data), or be offloaded to specialized accelerators. It also requires new design approaches in which monolithic applications 
can be decomposed into smaller components that may in turn be executed separately and on the most efficient resources. 
To address these needs we propose funcX---a high-performance Function as a Service (FaaS) platform that enables intuitive, flexible, 
efficient, scalable, and performant remote function execution on existing infrastructure including clouds, clusters, and supercomputers. 

funcX allows users to register and then execute Python functions without regard for the physical resource location, scheduler architecture, or virtualization technology on which the function is executed---an approach we refer to as "serverless supercomputing."
We have developed a prototype implementation of funcX and applied it to a range of scientific problems. We have also deployed it on two supercomputers, finding funcX to be capable of processing millions of functions and scaling to more than 65000 concurrent workers. 

Try it out at:
[https://funcx.org](https://funcx.org)

Further reading
- Chard, Ryan, Babuji, Yadu, Li, Zhuozhao, Skluzacek, Tyler, Woodard, Anna, Blaiszik, Ben, Foster, Ian and Chard, Kyle. "FuncX: A Federated Function Serving Fabric for Science." Proceedings of the 29th International Symposium on High-Performance Parallel and Distributed Computing. pp 65–76. 2020.K. 
- Chard and I. Foster. "Serverless Science for Simple, Scalable, and Shareable Scholarship." 15th International Conference on eScience (eScience). pp 432-438. 2019.
- Ryan Chard, Tyler J. Skluzacek, Zhuozhao Li, Yadu Babuji, Anna Woodard, Ben Blaiszik, Steven Tuecke, Ian Foster and Kyle Chard. "Serverless Supercomputing: High Performance Function as a Service for Science." . 2019.
- Skluzacek, Tyler J., Chard, Ryan, Wong, Ryan, Li, Zhuozhao, Babuji, Yadu N., Ward, Logan, Blaiszik, Ben, Chard, Kyle and Foster, Ian. "Serverless Workflows for Indexing Large Scientific Data." Proceedings of the 5th International Workshop on Serverless Computing. pp 43–48. 2019.
- Anna Elizabeth Woodard, Ana Trisovic, Zhuozhao Li, Yadu Babuji, Ryan Chard, Tyler Skluzacek, Ben Blaiszik, Daniel S. Katz, Ian Foster and Kyle Chard. "Real-time HEP analysis with funcX, a high-performance platform for function as a service." EPJ Web of Conferences. 245. pp 07046. 2020.

Funding

funcX is supported by NSF 2004894/2004932 and an Argonne Lab Directed Research and Development award.


