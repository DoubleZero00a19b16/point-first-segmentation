
# General

This repository shows the steps for point first segmentation with **ToF VL53L1X** and any a camera.

We will cover what is **Camera Calibration** and how to get **Camera Calibration Matrix** with opencv2.

# Camera Properties

To interpret with pixels on image plane, we have to know properties of it. There are 2 common terms **Intrinsic Calibration** and **Extrinsic Calibration**.

![Camera Parameters Calibration](https://github.com/DoubleZero00a19b16/point-first-segmentation/blob/main/camera_parameters_calibration.png?raw=true)

To make great understanding, let's split everything in parts.

* You can see, there are 3 Coordinate Systems, let's look them one by one. Camera Coordinate System is simply the world of camera (what camera sees and how it interpret with coordinates of a point on an object relative to its coordinate system. So, this coordinate system used for interpret the objects on image plane).
* Alright then, if we can see the image plane by using **camera coordinate system** why we need **image coordinate system**? So, it is so simple to understand, as mentioned we can just interpret with the obeject inside of the image plane, not the pixels on the image. Units of Camera coordinate system and image coordinate system are different, mm and pixel respectively. Moreover, camera coordinate system sees the everything in 3D; however, image plane is 2D. As a result, change in unit and dimension is enough to make a transformation to image coordinate system.
* It does make sense finding the exact pixel relative to the image coordinate system by using the coordinates of an object relative to camera coordinate system. This is what we call ***Intrinsic Calibration***, *(Intrinsic Calibration is to find the Coordinates of the pixel corresponds to Coordinates of a point on an object relative to Camera Coordinate System).* The matrix that responsible for transformation between Camera to Image is called **Intrinsic Matrix**
* After understanding Intrinsic Calibration, it is so easy to make reasoning about **World Coordinate System**. It is just coordinate system at somepoint in the area (it can vary relative to the application). Let's assume we know the coordinates of a point on an object relative to World Coordinate System. We want to know the coordinates of the corresponding pixel relative to Image Coordinate System. So, what to do is simply make a transformation matrix that transforms the World Coordinate System to Camera Coordinate System to make Intrinsic Calibration to get the coordinates of the pixel. Finally, the process of making transformation World to Camera, is **Extrinsic Calibration**, the matrix itself (Transformation matrix) is **Extrinsic Matrix**.

### Intrinsic Calibration

I won't talk about how to get the desired Intrinsic Matrix, instead we will directly use a tool to get that matrix.

https://github.com/paulmelis/opencv-camera-calibration/tree/main

The following github repo is doing exactly what I've said about getting matrix. Just print chessboard has 9x6 inner corners and took its pictures from different angels (more information and files are provided in repo).

At the end, the output of the python file will give you the **Camera Calibration Matrix**. WHAT IS IT? WE HAVE COVERED Intrinsic and Extrinsic, WHAT IS the Camera Calibration.

Don't worry about it, it is exactly what we need. The formula to get the coordinates of pixel by using the coordinates of a point on an object is:

$$s \begin{bmatrix} u \\ v \\ 1 \end{bmatrix} = \begin{bmatrix} f_x & 0 & c_u \\ 0 & f_y & c_v \\ 0 & 0 & 1 \end{bmatrix} [R \mid t] \begin{bmatrix} X \\ Y \\ Z \\ 1 \end{bmatrix}$$
