# Finding lanes on the road

## Writeup of the project
**The aims of this project are**
 
1. Create a pipeline for detecting the edges of the lane in which the car is travelling
1. Reflection about the choices made
1. Point out the shortcomings

*****

#### 1. How I created the image pipeline for lane edge detection
  1. First, create a copy of the image. This helps in us creating the final overlay.
  1. Convert the image to grayscale. This is required for Canny edge detection. Since most images are recorded in RGB channel, we used the COLOR_RGB2GRAY option in the grayscale function. Let's call this converted image gray\_image.
  1. Apply the Gaussian blur on gray\_image to reduce any noise. I chose a kernel size of 5 because most of the images that I'm working on are not that noisy. However, it is possible that some low-light images may be noisy and need a higher kernel size. Let's call this image gb\_image.
  1. We now apply the Canny edge detection algorithm on gb\_image. I've fiddled around with the values of the lower and upper thresholds, and arrived at the given choice based on what I felt gave me the best results. Let's call the resulting image of the Canny edge detection canny\_image.
  1. We will now create the region of interest in which we want to draw the lines of edge detection. This, hopefully, isolates the region of the image specific to our lane. For this, I created a new function image\_vertices, which takes in the width and height of the image, and returns a quadrilateral region of interest. The region of interest is created using fractions of the image width and height to take care of possibly different image sizes. After this region is created, it is superimposed on canny\_image to create an image that includes only the region of interest for further processing. Let's call this image roi\_immage.
  1. We now draw the lines on the lane edges of roi\_image. First, the Hough transformation is applied roi\_image. The image is returned with Hough lines drawn over the lane edges. Now, these lines are not joined, and extrapolations need to be done to achieve a continuous line. For this, I modified the function draw_line as follows
      * In order to join the line segments we need a single value of the slope. Given the possible minor numerical differences in the slope values, we need to compute an average slope of all the line segments. The slope of the left-side lane edge is less than zero, while that of the right-side lane edge is greater than zero. Thus, the average slope of the left side edge is computed using the slopes of the line segments of the left edge, and similarly for the average slope of the right side edge.
      * We now collect all the line segments belonging to the left side of the lane, and similarly to the right side of the lane. A single line is fitted through all the left edge segments and another single line through the right edge segments, using the fitLine function in cv2.
      * This slope and intercept of the fitted line is then appended to an array of the slope and intercept of the lines in the previous frames.
      * Once this array is available, we once again compute the average slope and intercept of the left and right lane edges. This average slope and intercept allows us to construct the one single line segment of the lane edge in the new frame. I use the slope and intercepts of the previous 3 frames to compute the average values for the latest frame. One can fiddle around with this values. However, do not include a lot of the past as the slopes may change rapidly along curves.
      * We can now draw the lines on each edge within the region of interest by computing the x & y coordinates of the lane edges using the coordinates of the region of interest, and the average slope and intercept of the new frame.
      * Let's call the resulting image of the Hough transformation and draw_lines function as lines\_img.
      * The code has description of the above steps in order for you to easily identify these segments.
      * Parts of this code was inspired by the work of Marcos Ottonello, which can be easily found on GitHub.
  1. The final step is to superimpose the lines\_img on to the original image (or frame) to get a frame of the original with lane edges drawn. This is achieved using the weighted\_img function. You can fiddle around with the weight parameters till you get a desired image.
  
The above pipeline is enclosed in the function image\_pipeline.
