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
## Point Cloud?
[![Video Title](https://img.youtube.com/vi/2crAfWZOgf0/0.jpg)](https://www.youtube.com/watch?v=2crAfWZOgf0)


## What is Point Cloud Registration?
Point cloud registration is the process of aligning or overlaying two or more 3D point cloud data sets captured from different positions or viewpoints into a common coordinate system.

![point_cloud_registration](https://github.com/vishapraj/Robot-Operating-System-ROS-/assets/126682925/5cc797bd-5ef1-4a3e-bba0-0d89e93e7fbd)

Imagine you have a room, and you want to create a 3D model of it using a laser scanner (like a LiDAR sensor). You scan the room from one corner, capturing a point cloud representing that part of the room. Then, you move to another corner and scan again, capturing a different point cloud from another viewpoint.
Now, you have two separate point clouds, each showing a part of the room from a different angle or position. To create a complete 3D model of the entire room, you need to align or "register" these two point clouds together accurately.

Point cloud registration algorithms try to find common features or overlapping areas between the two point clouds and use them to align the point clouds correctly. It's like finding common objects or structures (like a table or a window) visible in both point clouds and using them as reference points to match and overlay the point clouds perfectly.

## 1.Iterative Closest Point
One of the most widely used and simple methods for point cloud registration is called Iterative Closest Point (ICP). ICP uses the 3D coordinates (x, y, z) of each point in the two scans to try to match points between the scans. It starts with an initial guess of the displacement and then iteratively refines it by finding the closest points between the two scans and minimizing the distances between them.

![ICP_algorithm](https://github.com/vishapraj/Robot-Operating-System-ROS-/assets/126682925/56effbf1-b0fe-4d43-a6eb-cb7c90214c0c)

However, ICP and other point-to-point matching methods can struggle when the environment changes significantly between the two scans, either due to different viewpoints or changes over time (e.g., objects moving or being added/removed).

To address this, researchers have developed methods that rely on detecting and matching specific keypoints or features in the environment, rather than trying to match every point. These keypoints are selected because they are distinctive and likely to be visible and recognizable from different viewpoints or over time.
Some classical (hand-designed) methods for detecting keypoints in 3D point clouds include:

#### (A).Intrinsic Shape Signature:-
This method looks for points that have a large variation in the shape of their local neighborhood, making them distinctive and easy to recognize from different viewpoints.

#### (B).Keypoint Generator:-
This method selects points that have a high degree of "saliency" or distinctiveness based on their local neighborhood, making them stand out as potential keypoints.


Despite this extreme compression, the proposed approach can still achieve accurate metric localization and pose estimation by leveraging the learning-based object matching technique and robust pose estimation algorithms like weighted SVD or RANSAC. The key advantage of this approach is that it enables scalable mapping and localization for autonomous systems with limited storage and computational resources, while maintaining reasonable accuracy.

## Problem Setup:-
Step by Step Explanation:-

### 1.Object Extraction
The robot collects a point cloud, P 
s
​
 ={p 
i
​
 ∣p 
i
​
 ∈R 
3
 },which is a set of 3D points representing the environment from the robot's live sensor stream. The pre-built map of the city is another point cloud,P 
m
​
 ={p 
j
​
 ∣p 
j
​
 ∈R 
3
 }.

 ### 2. Goal: Estimating Transformation

 The Objective is to estimate the relative transformation T 
s,m
​
 =[R 
s,m
​
 ∣t 
s,m
​
 ],where 
𝑅
𝑠
,
𝑚
∈
𝑆
𝑂
(
3
)
R 
s,m
​
 ∈SO(3) represents the rotation and 
𝑡
𝑠
,
𝑚
∈
𝑅
3
t 
s,m
​
 ∈R 
3
  represents the translation. This transformation aligns the live point cloud 
𝑃
𝑠
P 
s
​
  with the map 
𝑃
𝑚
P 
m



## Example Scenario
Let's say the robot is navigating through a street and its live sensor stream detects several objects: lamp posts, trees, and buildings. The pre-built map also contains these objects.
### 1.Extract Key Points:-
From the live sensor stream, the robot identifies key points such as the tops of lamp posts, the corners of buildings, and specific trees. It does the same for the pre-built map.
### 2.Find Correspondences:-
The robot matches these key points between the live data and the map. For instance, it identifies that a specific lamp post in the live data corresponds to the same lamp post in the map.
### 3.Calculate Transformation:-
Using the Kabsch algorithm, the robot calculates the best rotation and translation that align these matched key points. This gives the robot its pose relative to the map.
### 4.Pose Estimation:-
Now, even if some objects in the environment change (like different cars parked on the street), the robot can still accurately estimate its pose by relying on the stable, semantic key points like lamp posts and building corners.
​
### To improve the process of estimating a robot's position using point clouds, we follow a method inspired by BoxGraph and SGPR. Here's a breakdown of how it works:
### 1. Semantic Segmentation:-
First, we start with a point cloud, which is a collection of 3D points representing the environment. Each point in the point cloud is assigned a semantic label using a pre-trained network. These labels classify the points into different categories, such as buildings, trees, or cars.

![Semantic_Segmentation](https://github.com/vishapraj/Robot-Operating-System-ROS-/assets/126682925/e05dc824-c4b7-4111-afd9-01c5885bef32)


### 2.CLustering into Objects:-
Using the Density-Based Spatial Clustering of Applications with Noise (DBSCAN) algorithm, we group the points into clusters based on their labels and their spatial coordinates. Each cluster represents an object in the environment, like a specific tree or a particular building corner.

![Clustering](https://github.com/vishapraj/Robot-Operating-System-ROS-/assets/126682925/23dd407e-5e50-45bf-ad32-af1dca25dcf6)


### 3.Extracting Key Information:-
For each cluster, we calculate its centroid (the average position of all the points in the cluster) and keep its semantic label. This gives us a set of labeled objects where each object is represented by its centroid and its semantic type.
### 4.Creating a Labeled object set:-


The result of this process is a labeled object set O={(o 
i
​
 ,l 
i
​
 )∣o 
i
​
 ∈R 
3
 ,l 
i
​
 ∈L}. Here, 
𝑜
𝑖
o 
i
​
  represents the centroid of an object, and 
𝑙
𝑖
l 
i
​
  is its semantic label. This labeled object set is used as the key points for further processing.

### 5.Simplified Approach:-
Unlike more complex methods that analyze the geometric structure within and between objects in the point cloud, our approach uses only the semantic labels and the spatial relationships between the objects. We then learn any additional representations needed for these objects.
 .
 
### Here's a step-by-step explanation of the approach:

### 1.Object Extraction:-
The Object Extraction step is a crucial component of the proposed approach, as it transforms the raw, dense LiDAR point cloud data into a compact and structured representation of individual object instances. This step involves two main substeps: semantic segmentation and instance clustering.


