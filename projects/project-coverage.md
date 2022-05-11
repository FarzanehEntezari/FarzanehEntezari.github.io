---
title: Complete Coverage Path planning
layout: page
---

## Intro

In the last decade, autonomous inspection and environment monitoring has gained great attention for various applications. Imagine a robot which is asked to periodically carry out a complete inspection in an environment and document the variations along the time. Such a fully automated monitoring mission by robots arises a variety of different challenges. We explore coverage planning tasks that are intended to generate mission plans in order to collect data from two-dimensional spatial fields. The objective is to prepare a detailed survey mission plan consisting of the sensing locations and the overall robot traveling path, such that the intended survey area is fully observed by the robot's sensor. Our ultimate goal is to survey the seabed and monitor the environmental processes in the ocean. Our emphasis on efficient coverage planning is motivated by the growing importance of the health of marine environments which need to be monitored repeatedly and consistently.


## Approach

We aim to generate a survey plan for seabed inspection by an Autonomous Underwater Vehicle (AUV), called Aqua. The task is to determine an optimal path that allows the robot to cover the entirety of the target area. In our problem, prior knowledge of the environment including a depth map of the seafloor is available.

The Aqua is supposed to navigate on a planar surface laying at a constant altitude above the surface of interest. Aqua robot is equipped with a down-looking sensor with a certain FOV able to image the seafloor from the navigating altitude. While a marine robot is navigating underwater at a constant depth, the sensor's FOV varies along the sea surface depending on the height of the target surface.

Considering that data collection by precise sensors on the AUV can not be done while the robot is moving, we focus on stationary sensor placement methods. We determine the best set of viewpoints that fully covers the target area and find the optimal robot path that visits all the viewpoints and covers the entirety of the area, in order to perform the survey with a shorter trajectory and fewer sample points while ensuring full coverage.

We presented a novel off-line sampling-based method for an autonomous underwater vehicle imaging the ocean floor. The proposed algorithm generates view configurations, differentiating between elongated areas and wide areas using the Voronoi skeleton, to achieve complete observability in the regions of interest. Next, we optimize the coverage route through the arranged viewpoints by solving a variant of traveling salesman problem.


## Experiments

The coverage planner algorithm is implemented in Python and runs on Robot Operating System (ROS). The algorithm is validated on a gazebo simulator by Clearpath Robotics Inc.

Our implementation handles range constraints and sight constraints by considering the occluded areas from each of the observation points.
The proposed algorithm is validated in simulation experiments and is proven to outperform previous approaches by improving coverage while reducing the number of scanning locations.