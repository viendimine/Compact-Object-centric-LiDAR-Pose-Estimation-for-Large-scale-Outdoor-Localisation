# Compact Object centric LiDAR Pose-Estimation for Large scale Outdoor Localisation
## What is Localization?
Localization is a crucial capability for mobile robots and autonomous vehicles to navigate safely. LiDAR sensors are widely used for localization due to their geometric nature and robustness to changes in lighting and appearance conditions. However, modern LiDAR sensors produce massive, dense point clouds containing tens of thousands of points, making the storage and transmission of these maps highly challenging, especially in large-scale environments.

## Problem Arised:-
Modern LiDAR sensors, which are commonly used in autonomous vehicles for perceiving the surrounding environment, can generate massive amounts of data. A single LiDAR scan can capture tens of thousands of points, where each point represents a precise 3D location in space. This high-resolution 3D point cloud data is crucial for accurate perception and mapping but comes at the cost of substantial storage requirements.
In the domain of autonomous driving, these storage requirements become even more pronounced. Autonomous vehicles rely on detailed 3D maps of the environment for localization, path planning, and navigation. These maps need to cover vast areas, potentially spanning entire cities or regions, to enable autonomous driving capabilities. As a result, the storage demands for these large-scale 3D maps can be substantial, requiring significant memory resources.


![VELODYNE-IMAGE](https://github.com/vishapraj/Compact-Object-centric-LiDAR-Pose-Estimation-for-Large-scale-Outdoor-Localisation/assets/126682925/71e67d8f-eedd-4af3-85b8-d624c48072a5)

Additionally, as the maps become more detailed and cover larger areas, the storage demands will continue to rise. Efficient compression techniques will be essential to manage these ever-increasing data volumes and ensure the scalability and real-time performance of autonomous driving systems.

## Solution Approcah:-
The proposed approach in this work aims to represent LiDAR scans in an extremely compact form while still enabling accurate localization and pose estimation. The key idea is to represent each LiDAR scan as a small set of 3D centroids and semantic labels corresponding to individual object instances detected in the scene.

![image](https://github.com/vishapraj/Robot-Operating-System-ROS-/assets/126682925/03be8f38-40ab-4ec6-8867-bdac41f029f4)


Here, we show that a descriptor composed of the positions
of the objects’ centroids and their class – i.e. three floating-
points and one byte – is enough for the task, requiring on
average 1.33 kB of storage per LiDAR scan against 1.41 MB
of raw data.

## What is Point Cloud Registration?
Point cloud registration is the process of aligning or overlaying two or more 3D point cloud data sets captured from different positions or viewpoints into a common coordinate system.

![point_cloud_registration](https://github.com/vishapraj/Robot-Operating-System-ROS-/assets/126682925/5cc797bd-5ef1-4a3e-bba0-0d89e93e7fbd)

Imagine you have a room, and you want to create a 3D model of it using a laser scanner (like a LiDAR sensor). You scan the room from one corner, capturing a point cloud representing that part of the room. Then, you move to another corner and scan again, capturing a different point cloud from another viewpoint.
Now, you have two separate point clouds, each showing a part of the room from a different angle or position. To create a complete 3D model of the entire room, you need to align or "register" these two point clouds together accurately.

Point cloud registration algorithms try to find common features or overlapping areas between the two point clouds and use them to align the point clouds correctly. It's like finding common objects or structures (like a table or a window) visible in both point clouds and using them as reference points to match and overlay the point clouds perfectly.




Despite this extreme compression, the proposed approach can still achieve accurate metric localization and pose estimation by leveraging the learning-based object matching technique and robust pose estimation algorithms like weighted SVD or RANSAC. The key advantage of this approach is that it enables scalable mapping and localization for autonomous systems with limited storage and computational resources, while maintaining reasonable accuracy.

### Here's a step-by-step explanation of the approach:

### 1.Object Extraction:-
The Object Extraction step is a crucial component of the proposed approach, as it transforms the raw, dense LiDAR point cloud data into a compact and structured representation of individual object instances. This step involves two main substeps: semantic segmentation and instance clustering.


