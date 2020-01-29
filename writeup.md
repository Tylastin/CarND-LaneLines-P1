# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road

The pipeline was tested on the images in the test_images folder. The corresponding output for each image can be found in the test_images_output folder. The pipeline was also validated on two videos, which can both be found in the test_videos_output folder.  

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale. Second, I ran the cv2 canny edge detection algorithm to obtain an image with only the edges(large gradient). Third, I used region masking to select the relevant region(section of the image where the lane lines are expected to be) and filter out the rest of the image. Fourth, I used the cv2 hough transform algorithm to detect the lane lines in the region masked edge lines image and obtain the end points of each detected line segment. Fifth, I extrapolated and averaged the hough line segments to draw a single line for the left lane line and a single line for the right lane line. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function. First, I calculated the slopes of all the hough line segments. I used the slope values to seperate the segments into left lane line and right lane line. Second, I weighted the lane line segments by length and used teh cv2.linefit() function to find a least squares fit for the left lane line and right lane line. I drew the best fit line from the bottom of the image up to the highest detected line segment.




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming is that when the car takes a sharp turn. The current implementation of linear extrapolation on the hough line segments would lead to innacurate tracking of the lane lines. 

Another shortcoming could be that if the lighting conditions change(such as during night time) the gradient might not be high enough at the lane lines to be detected by the canny edge detection algorithm alone. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use a second order interpolation so that the pipeline could more accurately track the lane lines of a curved road or a sharp turn. 

Another potential improvement could be to use color selection more effectively rather than relying on canny edge detection. If this change is made, the pipeline would be less sensitive to camera/lighting conditions. 
