---
layout: project
title: Wind Turbine Blade Optimization
description: MAE 4272 Final Report
technologies: [Matlab]
image: /assets/images/radio-machine-cad.jpg
---

Blade Design Final Report
MAE 4272, Fall 2025
Lab 408, Group 3, Blade 83
Ashley Padres, Julia Deffner, Ella Yellin, Anna-Sophie Schaldenbrand
December 12, 2025

1.  Executive Summary
This report outlines the process of designing and testing a small horizontal-axis wind turbine to maximize extracted power under an oncoming wind velocity distribution. Specifically, the wind turbine is optimized for use in an oncoming wind velocity of 4.8 m/s, the average velocity that would extract max power under its experienced Weibull distribution of velocities. To design the blade, a MATLAB model was developed to optimize the design. This included selecting an airfoil designation of NACA 4412, determining chord length and pitch as a function of radius, solving for the forces and stresses experienced by the blade, predicting output power curves, and iterating to determine the design angular velocity. The chosen design predicted a design RPM of 1050 that would extract 3.61 W at an oncoming wind speed of 4.82 m/s. The designed wind turbine was then tested at five different oncoming wind speeds, and experimental power graphs were recorded for each. Comparing the model predicted behavior with the experimental behavior, the actual wind turbine produced less power but spun faster, likely a result of the model’s assumptions. The maximum power extracted observed was 1.8 W at an oncoming wind speed of 5.8 m/s. Ultimately, while the wind turbine underperformed relative to what the model predicted, the performance demonstrates how optimizing the taper, twist, and CL/CD can result in a blade that maximizes power output under a Weibull distribution.