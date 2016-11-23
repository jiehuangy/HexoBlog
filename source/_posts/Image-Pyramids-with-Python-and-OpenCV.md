---
title: Image Pyramids with Python and OpenCV
date: 2016-11-23 17:13:56
tags:
categories:
---
![](/images/Image-Pyramids-with-Python-and-OpenCV-f1.png)

<!-- more -->
## [What are image pyramids?](http://www.pyimagesearch.com/2015/03/16/image-pyramids-with-python-and-opencv/)
An “image pyramid” is a **multi-scale representation** of an image. Utilizing an image pyramid allows us to **find objects in images at different scales** of an image. And when combined with a sliding window we can find objects in images in various locations.

At the bottom of the pyramid we have the original image at its original size (in terms of width and height). And at each subsequent layer, the image is resized (subsampled) and optionally smoothed (usually via Gaussian blurring).

## Image Pyramid with Python and OpenCV 
{% codeblock lang:python %}
import cv2

layer = 1
image = cv2.imread('image.jpg')
while True:
	cv2.imshow("Layer {}".format(layer), image)
	cv2.waitKey(0)
	layer += 1
	if(image.shape[0] < 50 or image.shape[1] < 50):
		break
	image = cv2.pyrDown(image)
{% endcodeblock %}

Result:
![](/images/Image-Pyramids-with-Python-and-OpenCV-f2.png)

Reference: [Image Pyramids with Python and OpenCV](http://www.pyimagesearch.com/2015/03/16/image-pyramids-with-python-and-opencv/)
