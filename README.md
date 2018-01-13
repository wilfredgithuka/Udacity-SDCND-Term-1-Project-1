# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_gray/solidWhiteCurve.jpg "Grayscale"
[image2]: ./test_images_blur/solidWhiteCurve.jpg "Blur"
[image3]: ./test_images_canny/solidWhiteCurve.jpg "Canny"
[image4]: ./test_images_region/solidWhiteCurve.jpg "ROI"
[image5]: ./test_images_merged/solidWhiteCurve.jpg "Hough"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

Generally I included another function drawLine() that would work with the draw_lines() function.
The drawLine() function has the line parameters for y=mx+c or b

lineParameters = np.polyfit(x, y, 1) 
    
    m = lineParameters[0]
    b = lineParameters[1]
    
    also with avarage values of y1 to x2
    
The draw_lines() function with use the drawLine to come up with the lines like the snippet below

drawLine(img, leftPointsX, leftPointsY, color, thickness)

## Loading Images
The first step was to load some specifcic python tools that I would use in my pipeline.
These were:

import random, from IPython.core.display import display, from IPython.display import display, HTML

These tools are very useful in the first part of loading the images and displaying them as
HTML in the Notebook. The images are now loaded, and the functions are set. Now to the main pipeline.

## Main pipeline

My pipeline consisted of 5 major steps namely:

* Grayscale
* Bluur
* Canny Edge Detection
* Masking
* Hough Transform

### Grayscale
![alt text][image1]
The Grayscale step is done using one of the provided functions in the helper functions:

* return cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)

I also had to create some new functions for Saving and Displaying the Grayscale images. This is my general Grayscale function:

* GrayImages = DisplayImages(TestImages, 'test_images_gray', TestImageNames, grayscale, 1)

### Blurr
![alt text][image2]
The Gaussian Blurr is simple and uses the function to produce a blurred images from the Grayscaled image. Here is my function, I used a kernel size of 15

BlurKernelSize = 19
Blur = lambda img:gaussian_blur(img, BlurKernelSize)
BlurImages = DisplayImages(GrayImages, 'test_images_blur', TestImageNames, Blur, 1) 

### Canny Edge Detection
![alt text][image3]
My Canny Edge Detector has a high of 100 and a low of 20.

### Region of Interest
![alt text][image4]

My region of interest worked preety well. I used the values that we had for the examples
and test.

### Hough Transform
![alt text][image5]

I used a hough transform with the following parameters:

rho = 1 
theta = np.pi/180 
threshold = 10     
min_line_length = 20 
max_line_gap = 1    

And the result is the image above. I managed to merge too.

Lastly I tested it on videos after modifying the draw_lines function.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the test images were changed with 
other images whose contast is different. No matter how much I teweaked my Canny edge detector, 
I still has issues detecting the lanes.

Corners: When the lane takes a corner, my pipeline gets 'lost' especialy in the last challenge.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to add more code to handle different types on image parameters.

Another potential improvement could be to work on the corners
