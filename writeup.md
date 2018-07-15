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

My pipeline consisted of 5 steps:

1. convert the image to grayscale
2. blur it with a gaussian kernel with size of 5 pixels
3. find the edges of the image with canny edge detection algorithm (low TH = 50, high TH = 150)
4. mask the image with a trapezoid that covers the interesting area of the image. paramaters were chosen in a trial and error process
5. Use Hough transform to find the lines among the edges. I chose minimum line length of 20 pixels and maximum gap allowed of 200 pixels. this is because of the way that striped lines usualy look.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. identify left or right lane: classify the detected lines according to angle and position related to image center.
2. extrapolate the lines in each group so the would go from bottom of image to the same height, and then draw their average on the image.

### 2. Identify potential shortcomings with your current pipeline


* Current pipeline doesn't take into account the expected color of the lines.
* The flow does not work well on sharp turns. the lines that I draw are in a fixed size, when there is a sharp turn the lines intersect.
* when moving from images to videos, the line is not stable.


### 3. Suggest possible improvements to your pipeline

* add a block that removes all pixels which a re not in shades of white or yellow
* instead of extrapolating all the lines into an average line, we might try to use a higher degree polynom, and then we can handle road curvature in a better way.
* use time based averging between frames so we can get a more stable video.
