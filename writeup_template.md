# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


Video Result:

[Challenge Video](https://youtu.be/KVWa5f-PTcM)

[Solid White Right](https://youtu.be/eoJn3ycHCfU)

[Solid Yellow Left](https://youtu.be/ourvg-1_RSQ)

An approach to make static lines length:
[Static Lines](https://youtu.be/Yy8vs14vWkg)

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 main steps.

1. Convert RGB image into grayscale

2. Gaussian Smoothing

3. Cany Edge Detection

4. Region of Interest

5. Hough Transform

6. Weighted Image

In order to draw a dynamic lines on the left and right lanes,I modified the draw_lines() function and added a new function called normalized_lined(). In modified draw_lines() function, I calculate the slope to know which segments are a part of left lines and right lines. After I calculate the slope, I make a further calculation by using the slope to find the angle. THe idea is, I want to decide in which range of angle is eligible to be a part of left and right lines. Furthermore, I that it's quite useful for the challenge section, because it helps me to avoid this error, **"Python int too large to convert to C long"**. After that, I append each lines into a new array, to know which part is X_left, X_right, Y_left, or Y_right. Then, I continue it by normalized the result in normalized_lines() function.

In normalized_lines() function, I try to attain the coefficient of x and y by using **np.polyfit()**. Then, I use the result of it to calculate top_x and bottom_x. Nothing to forget, I need to change the result from float type into int type. In order to answer the challenge, I use a dynamic top_y by taking the average of all specified lines. Thus, it would be re-adjusted everytime there're short of long straight lines like in the challenge video.
Here are the results:

![Solid White Curve](https://github.com/weisurya/nd013-Finding_Lanes_Lines/test_images_output/solidWhiteCurve.jpg)

![Solid White Right](https://github.com/weisurya/nd013-Finding_Lanes_Lines/test_images_output/solidWhiteRight.jpg)

![Solid Yellow Curve](https://github.com/weisurya/nd013-Finding_Lanes_Lines/test_images_output/solidYellowCurve.jpg)

![Solid Yellow Curve 2](https://github.com/weisurya/nd013-Finding_Lanes_Lines/test_images_output/solidYellowCurve2.jpg)

![Solid Yellow Left](https://github.com/weisurya/nd013-Finding_Lanes_Lines/test_images_output/solidYellowLeft.jpg)

![White Car Lane Switch](https://github.com/weisurya/nd013-Finding_Lanes_Lines/test_images_output/whiteCarLaneSwitch.jpg)


### 2. Identify potential shortcomings with your current pipeline

Two potential shortcoming would be the line length that will not be the same and the lines would not look like a single line because I make it become as dynamic as possible to answer the challenge video. However, the result still could not as smooth as the example output. Furthermore, this hyperparameters are hardly hand-written, which still could not re-adjusted this algorithm faces a different kind of field (cloudy, night, fog, etc). I found out that I need ro re-adjust the hyperparameters multiple times in order to reach this kind of output.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to improve this algorithm which further knowledge that I may learn from the next section. I found that with only using this kind of algorithm, it still could not face any kind of condition in the environment.

Another improvement is to find a way to make sure that, even though the lines are dynamic, it would only show 1 line for each side, and make the transition as smooth as possible.