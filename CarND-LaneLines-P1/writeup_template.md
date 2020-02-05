# **Finding Lane Lines on the Road**
---
**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Conclude the work in a written report

![Ultimate result](./examples/laneLines_thirdPass.jpg "Grayscale")

---

### Reflection

### 1. Pipeline Overview

My pipeline consisted of 5 steps.
* First, I converted the images to grayscale
* Then I filtered out noise using OpenCV GaussianBlur function given a kernel size
* Thirdly, I applied the canny transform given a high and a low threshold in order to detect edges
* Fourthly, I filtered out edges outside of a predefined region of interest
* Lastly, I extraced all the lines to be drawn from the image based on hough transform using the OpenCV HoughLinesP funciton.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first grouping all the line segments into two groups after all the line segment centers and slopes are calculated: line segments with positive slopes within a threshold is categorized as the right group whereas line segments with negative slopes within a threshold is categorized as the left group. Please note that top-left corner of the image has coordinate of (0,0). Going right, the x axis becomes positive. Going down, the y axis becomes positive.

After all line segments are grouped into left and right lanes, an average center and slope are calculated for each group. Then a specified height on the image that the lane lines could reach upmost is defined. Given this specified height and considering that the lane lines will be ended at the bottom edge of the image, the two endpoints of the left and right lane lines could be calculated based on the calculated average center and slope. Then the lines could be drawn based on the calculatd two endpoints of the lanes.

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lane is not confined by straight lines. Instead, the lane lines could be curves when the car is in a turnning. Plus, the region of interest might not be in the mid-bottom part of the image.

Another shortcoming could be that the lane lines might not be ended at the middle part of the image. The predefined specified height might not be flexible enough to fit all cases.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use higher order polynomial to curve-fit the lane lines, instead of just using linear model.

Another potential improvement could be to se the steer turning data to dynamically adjust the region of interest when the vehicle is turning.