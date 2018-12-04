# Object-Tracking

As a major part of my internship in summer 2018, we worked on the detection and tracking of vehicles from a set of video feeds provided to us by the company.
The problem was mainly divided into 2 parts :
### 1. Detection of the Vehicles from the video:
Here, we have presented the code for general object detection which can later be used for custom objects. Y.O.L.O v3 (You Look Only Once) frame work was adopted to perfrom object detection. Initially, Y.O.L.O v3 which utilizes Darknet Convolutional neural network framework was developed on C language so it was difficut to map the code into python environment. However, some developers have successfully compiled Y.O.L.O v3 in python. Y.O.L.O v3 has pre-trained weigths for detection of many common objects. Furthermore, it is capable of performing mutliobject detection in a given frame which is highly useful for our use-case, Vehile detection. However, darknet requires very high processing speeds which is why I was only able to run the framework at 4-5 fps. on a machine having NVIDIA GTX 1050Ti GPU.   
For more information on how to use Y.O.L.O v3 on python, I highly recommmend you to visit : https://github.com/madhawav/YOLO3-4-Py

### 2. Track Vehicle Object through the span of the Video:
Once, Object is detection is done, A major issue with almost all detection algorithms is that they often tend to lose the contact of some objects in some video frames. So, It becomes difficult to ID such objects throughout the video-feed. In order to keep track of such objects through the video and keep mapping the unique IDs of each objects, many object tracking algorthims have surfaced. One such algorithm is Kalman Filters. 
#### Kalman Filters:
Kalman filter predicts values using a bunch of mathematical equations under the assumptions that our data is in the form of Gaussian Distribution and we apply linear equations to that Gaussian distribution. But that is not always the case. In real world, we have non linear equations, here a filter called the Extended Kalman Filter can help. EKF takes helps of Taylor Series (and Jacobian Matrix further) to linearly approximate a non-linear function around the mean of the Gaussian and then predict the values.
But, we are using the Unscented Kalman Filter (UKF). We use it because it is able to give a better performance than an Extended Kalman Filter could. Unscented Kalman Filter has a concept of Sigma Points. We take some points on source Gaussian and map them on target Gaussian after passing points through some non linear function and then we calculate the new mean and variance of transformed Gaussian. It can be very difficult to transform whole state distribution through a non-linear function but it is very easy to transform some individual points of the state distribution, these individual points are sigma points. These sigma points are the representatives of whole distribution. 
When a Gaussian is passed through a non-linear function, it does not remains a Gaussian anymore but we approximate the Gaussian from the resulting figure, so in UKF a process called Unscented Transform​ helps us to perform this task. To summarize here are the below steps the unscented transform performs:
1. Compute Set of Sigma Points
2. Assign Weights to each sigma point
3. Transform the points through non linear function
4. Compute Gaussian from weighted and transformed points
5. Compute Mean and Variance of the new Gaussian.
For detailed information on basic kalman filters and it's working:

[![IMAGE ALT TEXT](https://user-images.githubusercontent.com/22682743/49422066-4fd1e900-f7b8-11e8-9dc7-79d91d11b798.png)](https://youtu.be/CaCcOwJPytQ?list=PLX2gX-ftPVXU3oUFNATxGXY90AULiqnWT "Special Topics - The Kalman Filter (1 of 55) What is a Kalman Filter?")

To understand more about the working of Uncented Kalman Fitlers please visit: https://goo.gl/aoQpqE
## Note
Before you run the project, make sure your system meets the following system requirements:
1. Ubuntu 16.x (Not Ubuntu 18.x) as darknet requires g++ version 6 or less.
2. GPU NVIDIA GTX 940 or higher. Still it may run on a very low FPS.
3. Unfortunately, at the time of creation of this project, Y.O.L.O v3 for python was not running on windows OS. So you may check out the latest version by visting the abouve mentioned link in 1st part.



