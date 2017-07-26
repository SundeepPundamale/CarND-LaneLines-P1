# **Finding Lane Lines on the Road** 

## Writeup Template
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:

* Make a pipeline that finds lane lines on the road
* Extrapolate the lanelines and draw them on the image
* Once the pipeline is working try it out on a video
* Connect/avearge/extrapolate line segments to the output like [image2]



[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./examples/laneLines_thirdPass.jpg "thirdpass"

---

### Reflection

### 1. Description of my pipeline. 

Building my pipeline consisted of the following steps:

* Ensure that my project environment is set up correctly such as setting up the Anaconda environment, ensure all the dependencies are installed correctly and no import errors appear while executing the Jupyter cells and the required project folders such as "test_image_output" and "test_videos_output" are created

* Next I convert the test image to grayscale, using the grayscale() function

* After converting the image to grayscale i apply Gaussian smoothning using the gaussian_blur() function. This step helps in supressing the noise and averages the spurious gradients

* Now i apply the canny edge to the image using the canny() function

* Next I eliminate the parts of the image which is not of interest to detect lanes using the region_of_interest()  function 

* Next i apply the Hough Tranform using the hough_lines() function to find the lines on the masked image 

* Next i merge the output of hough transform with the original image to represent lines on it with the weighted_img() function

* Finally, i loop through the "test_image" directory to pass each image in the folder through the pipeline and save the output in the "test_images_output" directory 

* In order to draw a single line on the left and right lanes, I modified the draw_lines() function by iterating through each line and calculate the slope and center, then seperate the right and left lane by measuring the slope, then average the center and slope values. Now the objective is to find the new (x1,y1,x2,y2) values. By using center and slope values 
and fitting to the bottom of the image and the specified height the new (x1,y1,x2,y2) are derived using the following equation:  (y-y') = M (x-x')


### 2. Identify potential shortcomings with your current pipeline
* The min and max line gaps are hard coded, the current pipeline might not be re-suable in scenarios where the line gaps are too big
* Another shortcoming could be with selecting region of interest. In case of a de-tour or a sharp curve in the road the pipeline might not be able to identify left and right lanes


### 3. Suggest possible improvements to your pipeline
* Avoid hard coded values or find possibilities to have various scenarios covered so that the min and max line gaps are fail proof

* In my implementation the region of interest is a triangle. In real world scnearios the car is not always positioned in the center of the road, between two parallel lane markers. A potential improvement could be in designing the region of interest for variious real world scenarios


