# **Finding Lane Lines on the Road** 

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

My pipeline consisted of 5 steps. 

1. First, I converted the images to grayscale, 
2. Gaussian filter applied to the grayscale. The kernel size used is 5, similar to the exercises from the lesson. 
3. Canny edge detection algorithm applied to the gaussian result using thresholds 50 and 150.
4. Hough lines extracted from the canny edge image using the following parameters:

rho = 1 # distance resolution in pixels of the Hough grid
theta = np.pi/180 # angular resolution in radians of the Hough grid
threshold = 20     # minimum number of votes (intersections in Hough grid cell)
min_line_length = 30 #minimum number of pixels making up a line
max_line_gap = 3    # maximum gap in pixels between connectable line segments
5. Applied a region of interest mask to the image so that only the interesting lines are shown.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by getting the average slope of the lines sloping left (right lanes) and sloping right (left lanes)
Then, I used the formula y = mx + b to calculate the start and end x,y coordinates based on the size of the image and the mask used.

Screenshots of the pipeline can be seen in the cell 5


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there's snow on the ground (or a lot of dirt)

Another shortcoming could be when there are tire/skid marks - they might be picked up as lanes. 

Also, this will definatelly not work when there's temporary lanes in construction sites.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to add color detection to the pipeline. This will eliminate some false positives, such as skid marks and shadows.

### 4. Challenge
At first sight, it seems like the challenge video has a different resolution than the rest. Simply moving the area of interest to the center of the creen will probably solve the challange too. 

An approach will be to assume that the are of interest is always centered, and that it goes about 50% up on the image.
