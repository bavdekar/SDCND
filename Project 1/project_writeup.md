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
  1. We will now create the region of interest in which we want to draw the lines of edge detection. This, hopefully, isolates the region of the image specific to our lane. For this, I created a new function image\_vertices, which takes in the width and height of the image, and returns a quadrilateral region of interest.
  
  #### 2. Possible shortcomings
  1. This program uses the RGB information of the images to convert it to grayscale. Grayscale intensity is a function of the values of R, G, and B of the pixel. These values are prone to the kind of lighting available when the video was shot. Hence, the performance of this algorithm cannot be guaranteed across different lighting conditions. I hope, as the lessons progress, we come to know about how to handle different lighting conditions.
  1. This algorithm hasn't been tested for night time videos or low light videos, which tend to be more noisy. Hence, I believe further tuning of the algorithm may be required for these conditions. In fact, an adaptive tuning, which is a function of light intensity is a good way to make sure maximum information is extracted under different lighting conditions.
  1. What if some sections of the lane edges are missing? This is demonstrated in the optional challenge video, and this algorithm doesn't perform great in that scenario.
  1. Again, this algorithm hasn't been tested for tight curves, so the region of interest may need to be defined by a polygon with more than four sides to improve its accuracy.
  1. One bug in my own coding is that the Canny edges are still visible in the final video. I'm trying to remove those, and suggestions to achieve that are welcome.
