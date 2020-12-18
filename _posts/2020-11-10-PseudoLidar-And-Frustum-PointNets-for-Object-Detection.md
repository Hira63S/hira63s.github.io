---
layout: post
title: PseudoLiDAR and 4D Object Detection
subtitle: First post in 4D object detection with PseudoLiDAR Input Series
gh-repo: Hira63S/Tesloyta
gh-badge:
  - star
  - fork
  - follow
tags:
  - object-detection
  - Computer Vision
  - PyTorch
  - SqueezeDet
comments: true
---
#PseudoLiDAR Approach

Computer Vision has been a hot topic of discussion because of the hype around it's potential uses from autonomous cars to drones delivery and everything in-between.. When it comes to its application in autonomous cars, we have seen a shortcoming with the input format from camera i.e. images. Because of their two dimensionality, while object detection is quick and easy, there are a lot of edge cases that limit our ability to get 100% accuracy for the risky task of autonomous driving. There have been a lot of alternatives introduced that try to overcome the shortcoming of 2D object detection. One of those alternatives is the introduction of PseudoLiDAR where we convert the information incoming from cameras i.e. images or videos into 3D point clouds and then, run the 3D object detection networks on those PseudoLiDAR representations.

##Background:

 The PseudoLiDAR paper uses PSMNet model to first train the model on disparities between stereo images but this technique could also be used for monocular images. The outptut of the disparities is then converted into PseudoLiDAR representations. The object detection model Frustum PointNets, then takes as input the predicted point clouds to make 3D object detection on PseudoLiDAR point clouds.


##Challenge:

The 4D Sptio-Temporal Object Detection makes use of Minkowski Engine Library that is designed for processing Sparse tensors. Goal is to perform ablation study to see whether the Frustum PointNet approach is better than the Sparse Tensors approach. The details about these models and how they approach the problem of 3D object detection and then, 4D object detection will be discussed in the future posts.
