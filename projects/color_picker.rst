.. role:: raw-html-m2r(raw)
   :format: html


RPL Color Picker
================

The RPL Color picker system is designed as a test system for integrating machine learning and optimization techniques with the robotic experimentation available in our workcell. The system chooses a random target color, and then runs one of a number of different optimizers to find the optimal combination of 3 differently colored liquids to most closely match that color.  The colors are mixed using the robotic workcell in RPL, allowing for continuous running and higher throughput. The system is intended as a demonstration of the RPLs ability to facilitate automatic discovery.

.. image:: /images/projects/ColorPicker.jpg



`Running Instructions and Further Info <https://github.com/AD-SDL/rpl_workcell/tree/main/color_picker>`_

Modules (in order of use in workflow):
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* `Hudson Sciclops <../modules/hudson_plate_crane.html>`_
* `PF400 <../modules/pf400.html>`_
* `Opentrons OT2 <../modules/OT2.html>`_
* `Camera Module <../modules/camera.html>`_