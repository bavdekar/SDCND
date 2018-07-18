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
      * First I compute the average slopes
