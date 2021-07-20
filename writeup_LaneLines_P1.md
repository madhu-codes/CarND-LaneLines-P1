# **Finding Lane Lines on the Road** 


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road.
* The pipeline takes an image as an input, and then using the image processing techniques presented in lesson 1 identifies the lane lines and then 
* draws the lane lines on the original image. 
* The test images and videos provided have been processed in this pipeline and the outputs are located at CarND-LaneLines-P1/test_images_output and 
* CarND-LaneLines-P1/test_videos_output


### Reflection

### Pipeline Description: My pipeline consists of the following steps:
- Make a copy of the original image
- Convert the image to grayscale
- Gaussian blur on the grascale image
- Apply the Canny function on the blurred image to find the edges
- Select the region of interest (roi) and mask out the rest of the image
   Here a triangular region which contains the bottom half of the image is considered as the roi
- Define the Hough transform parameters (the code has been commented to indicate the chosen parameters for the Hough Transform)
- Run Hough on the detected image
- Overlay the hough lines image on the original image


In order to draw a single line on the left and right lanes, I modified the draw_lines() as follows:
 - Classified the line as belonging to the left or right lane marker based on the sign of the slope (positive slope = left lane; negative slope = right lane)
 - Calculated the y-intercept for each line
 - Calculated the average of all slopes that belong to the left lane marker and right lane marker respectively. 
   Only slopes that lie within a reasonable range (+/- 0.15 and +/- 0.85) were considered for calculating the average
 - Calculated the average y-intercept of all lines belonging to the left and right lanes respectively
 - Fixed the y-coordinate for the top and bottom of the region of interest and then calculated the corresponding 
   values of the x-coordinate using the average slope and average y interept values
 - Drew the lane line with the fixed y-coordinate and corresponding x-coordinates that were calculated in the previous step


### 2. Potential shortcomings with my pipeline:
 - It does not work well when lane lines have a high curvature (it does not work at all with the video challenge)
 - Not robust since the average slopes across the different frames of the video are not take into account, making the lane lines jump around a bit


### 3. Possible improvements to the pipeline:
 - A possible improvement would be to store the average slope and y-intercept values across the frames and then take the average so that we use the 
   history across the frames, making it more robust.

