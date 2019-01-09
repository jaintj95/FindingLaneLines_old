# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps: 
1) First, I converted the input image to grayscale

2) Applied Gaussian blur to the grayscale image to remove noise

3) Then I applied Canny Edge Detection to detect edges in the image

4) Added a mask to the image that retains our region of interest and blacks out other regions

5) Applied Hough Transform to detect lines in the image

6) Overlap the output image over the initial image to generate final images


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:

1) Initializing empty lists to store left/right X and Y coordinates

2) Calculate the slope of each line and appending the coordinates to left line list if the slope is negative,
and right line list if the slope is positive
    2.1) For left lanes, I am also discarding all x coordinates that lie in the right half of the image and vice-versa

3) Add an additional helper function that calculates the average of all coordinates and then fits a line to the X and Y points.

4) Calculate the final points x1, y1 and x2, y2 using appropriate equations

5) Draw a line using the final coordinates calculated above


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when too much light or shadow is casted on the lanes. This would generate noise in the images. The RGB space is limited in this sense. 

Another shortcoming could be detecting lane lines on curved roads. Our current implementation focuses on drawing a straight line but this pipeline will fail when curved lane lines are encountered.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to convert the image to alternate colour spaces such as HSV or HSL to overcome the limitations of RGB space.

References used:
1) Numpy polyfit function - https://peteris.rocks/blog/extrapolate-lines-with-numpy-polyfit/
( I am not using this function in the revised project)