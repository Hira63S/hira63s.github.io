---
layout: post
title: PseudoLiDAR and Frustum PointNets for 3D Object Detection
---

# PSMNet-Argo

3D object detection has been deemed a crucial task in autonomous driving. So far, Lidar has been the go-to technique for collecting 3D point clouds and using 3D object detection models for inference on them. Recently, however, we have seen an increase in research on [PseudoLiDAR](https://arxiv.org/pdf/1812.07179.pdf) techniques that focus on creating point clouds using input from camera streams. Here is how the pipeline is:

1. The point clouds from the dataset are used to generate disparity using stereo images.
2. The model is trained on those disparities so that at test time, we can get stereo images and predict the disparity between pixels in left and right images.
3. The disparities are then converted into, PseudoLiDAR point clouds for 3D representation using the techniques described in the [PseudoLiDAR](https://arxiv.org/pdf/1812.07179.pdf) paper.

After the point clouds can be predicted from stereo or monocular images, any 3d object detection model can be used to make inference on the PseudoLiDAR Point clouds. The gap between the accuracy of 3D object detection models on Lidar and PseudoLiDAR point clouds is closing fast. A lot of research is being conducted on improving and further developing these techniques because cameras are a great alternative to Lidar because of the factors that make Lidars not an ideal option for scaling autonomy. One of the reasons is the cost, the point clouds are noisy and the cameras also manage to operate at a high frame rate and provide denser depth maps compared to 64 or 128 sparse rotating laser beams from LiDAR.

The next step after the generation of LiDAR point clouds is the training of 3D object detection model. Here, we can use any model that was designed for training on the LiDAR point clouds. It's simpler and easier because most of the models only use the {x, y, z} coordinates of the points from point cloud to train the model. There are, however, multiple techniques to data representation that are used in training 3D object detection models.

The 3D data is much more denser than the 2D images: 1024x1024 image with 3 channels compared to 3D data with {x, y, z} axis for each point in the point cloud. Moreover, running convolutions on 2D verses 3D data leads to exponential increase in parameters: 2D convolution with kernel size 5 requires 5**2 = 25 weights increases exponentially to 5**3 = 125 in a 3D cub and to 625 for a 4D tesseract. For that reason, there have been multiple techniques to developed from different way of representing the data to different ways of making predictions.

Two main techniques that I have been working with are Frustum PointNets and SparseNets. [PointNet](https://arxiv.org/pdf/1612.00593.pdf) was developed to process point clouds for 3D classification and segmentation where it takes in points from the point cloud and outputs either class labels for the entire input or per point segment/part labels for each point of the input(segmentation). The network focuses on max pooling where it learns functions/criteria that select interesting or informative points in the point cloud and encode the reason for their selection.
