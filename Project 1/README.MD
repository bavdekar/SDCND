# The Lane Detection Project

### This is the first project that I completed as a part of the nano-degee programme.

The first thing about driving cars is safety. One important aspect of safety is to drive within your designated lane (unless changing it). When humans drive, their eyes can see the edges of their lane and periodically steer their car so that it stays within the two edges of the lane. Our eyes can easily see the edges, and our brain can easily interpret that those edges shouldn't be crossed. Thus, the challenge for autonomous cars is to, first, be able to see the road, and second, detect the edges of the lane.

In this project, I have implemented a lane-edge detection algorithm using Python and its associated packages. This README file will guide you through how the lane detection is achieved.

#### 1. Environment and required packages
The project was completed in Python programming language using Jupyter notebook. I run Jupyter and Python using the Anaconda environment. You can install Anaconda for Windows10 or other supported OSes from [Anaconda's website](https://www.anaconda.org). I use Python3 and its updated versions. This code will work for Python3, but I don't guarantee that it _will work_ in Python 2.7. To use this code, and run it you will need to install the following packages: **OpenCV**, **moviepy**, and **msgpack**. These packages mostly never included in the default Anaconda Python installation. The installation requirements and instructions provided here are only for Anaconda on Windows10. If you are using a different OS, look up for instructions specific to your OS.

To install OpenCV, open the Anaconda command prompt (as administrator), and type: `conda install opencv`. Repeat this for _moviepy_ and _msgpack_.

#### 2. Running the code
Open Jupyter notebook by typing `jupyter notebook` at the command prompt. This should open Jupyer in your favourite browser. From there you can navigate to the folder that holds all files. Locate the file **P1.ipynb**, and open it. You can now run this code one cell at a time or all cells together. Make sure that none of the packages are missing, otherwise the code will break down. If you want to add any test images add them to the folder _test\_images_. Similarly, additional videos must be added to the folder _test\_videos_. The program is coded to detect images and videos in these two folders only.

