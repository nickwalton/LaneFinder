## **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road

[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight.jpg

---

![alttext] [image1]

### Pipeline

### 1. Pipeline Layout

1. I converted the image to grayscale and performed gaussian smoothing on it. \n
2. I ran a canny edge detector algorithm on the image to identify the edges.
3. Defined the region of interest, a 4 sided polygon and masked everything else from the image 
4. I used a hough transformation to find the different line segments remaining in my image. 
5. To extrapolate these line segments into a single lane I used the np.polyfit function to perform linear
  regression on the endpoints of the lines sorting them into right and left lanes based on the slope
6. Finally I created a weighted image to merge the extrapolated line onto the original image augmenting it witht eh 
  algorithm's understanding of where the lanes are. 

### 2. Identify potential shortcomings with your current pipeline and suggest possible improvements

One potential shortcoming of my algorithm is the way I extrapolated the lane from line segment endpoints is very sensitive to noise. A tiny line segment has the same weight in the algorithm as a line segment that covers the whole lane. With more time this is one aspect that I would want to fix. I could do this by writing my own linear regression function that like polyfit and implementing it in such a way that I can input lines and give greater weight to longer lines in the function. Another way I could fix this is by duplicating the points that I feed the polyfit function based on weight, adding more of the same points for longer lines etc...

Another shortcoming with this approach in general is having a static high threshold for the canny edge detector will likely fail in different conditions, for example at night, in the rain or snow etc.... this isn't a robust way to identify the lines unlesss there is some way to dynamically modify it or check it in some other way. Some possible solutions inlude checking the change in the lane line each slide to get an idea for how much error there is eliminating new line segments that are two far different from the previous lane in the calculations etc...

