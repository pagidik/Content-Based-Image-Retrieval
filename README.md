# CONTENT BASED IMAGE RETRIEVAL

The overall task for this project is, given a database of images and a target image, find images in the data with similar content. 
Instead, will focus on more generic characteristics of the images such as different color spaces, histograms, spatial features, and texture features.


This repository contains 7 files. Each file executes the a particular task.
To execute a particular fille, the file name along with the filter.cpp file should be added in the executable list in the CMakeLists.txt file. 

Project Report Wiki Link: 
https://wiki.khoury.northeastern.edu/x/Yo55Bg


In each of the files, the user can change the input target image name in the code. 

The first task executes the baseline matching using the 9 x 9 patch at the center of the image. 

The second task is divided into two files, 2a and 2b. 2a is for 2D histogram and the latter is for 3D histogram.

The third one is for multihistogram macthing in which the image is divided in two equal halves (upper and lower). 
These two are taken as a features and computed the distance metric. The method used to compute the distance is Histogram intersection.

Task 4 is analyzing texture and color. In this the texture feature is computed based on the histogram of the gradient magnitude of the image. 
the distance  metric used here is the weighted sum of the both texture and color histograms. 

In task 5, the custom design and one of the extension is included (create additional features and matching method).
The image is converted into the HSV color space and it is masked with a particular color values which generates a binary image.
the magnitude of the single channel binary image is computed to analyze the shape of the object.
For this a new sobel and magnitude functions were defined to compute on a single channel image.
The histogram of the binary image and the magitude is computed. Further the spatial variance is computed for each histogram which are being used as features for the distance metric. 

This method is useful for images which have a defined shape in any orientation and have texture in it. 
The best example for this is filter is a spherical ball with texture. the basketball image is the best fit and this method can detect decent amount of balls from the database. 


Another extension is to detect as many blue bins as possible. 
For this task, The image is converted in to the HSV color space and filtered the color space to blue. 
This generates a binary image of single channel. inspired from the learnings, from task 5, The histogram of this binary image is computed.
Since the blue bins are plain without texture, computing magnitude could have resulted in diverse results.

Since the bin is located in one place, the spatial variance of the histogram will result in small values. 
So I have used the sum of squared differences of color histogram and the spatial variance as two features for computing the distance metric.
This resulted in 8 blue bins/mail boxes in the top 10 results and other blue objects in the top 20.
Also since the image is converted in to a binary image in the begining itself, the computation time is so much faster.
