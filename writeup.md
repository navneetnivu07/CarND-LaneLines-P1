# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

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

1. I converted the images to grayscale

2. Then, I applied gaussian smoothing using the ```cv2.GaussianBlur()``` with the kernel size of 13

3. Then, I applied canny edge detection using ```cv2.Canny``` with low threshold of 20 and high threshold of 100

4. Next, keep only the region of interest and masking the rest of the image

5. Then, I applied the Hough Transform to identify lines

6. Then, Converting the lines into straight lines

7. Then, Smoothing the shaky with average filter

8. Finally, Plotting the lines on top of the original image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 

1. Seperate the right line and left line using slope

2. Pass the x and y points to the new funrtion `drawLine()`

3. Find the slope and intercept for each set of points

4. Get new slope and intercept by taking average of last 15 points to remove shaky lines. I created a collection to store previous m & b values.

5. Difference between consecutive points is stored in a seperate list for plotting to find the sudden spike in change of m & b

6. Those spikes, i.e. error lines are removed and m & b is updated

7. Finally the extended line is plotted using new slope and intercept value.

### 2. Identify potential shortcomings with your current pipeline

The draw line function if not general for all lane detection videos.
Few boundrary cases and filters are added specific to solve the provided videos with max accuracy.

By taking the avarage of last few frames would be fine for straight lanes, it struggles with the optional
third video where there is a curve.

The pipeline detected few horizontal lines which are not actual road lanes, in the optional third video the shadows and reflection affect the pipeline. 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to generalize the optimal values in smoothing, hough transform and moving average for 
any lane detection video.
 
Boundary conditions specific to provided videos can be removed by dynamically updating the values from previous calculation.

Pipelines needs improvement in finding lanes in curved roads.
