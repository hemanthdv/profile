---
layout: post
title: Office-Home Dataset
description: "Object Recognition dataset for domain adaptation experiments"
comments: false
---

The Office-Home dataset has been created to evaluate domain adaptation algorithms for object recognition using deep learning. It consists of images from 4 different domains: Artistic images, Clip Art, Product images and Real-World images. For each domain, the dataset contains images of 65 object categories found typically in Office and Home settings.

<br />
<br />
<img align="middle" width="100%" src="{{ site.url }}/images/DataCollage.jpg" alt="...">

<em>Figure 1: Sample images from the **Office-Home** dataset. The dataset consists of images of everyday objects organized into 4 domains; \texttt{Art}: paintings, sketches and/or artistic depictions, \texttt{Clipart}: clipart images, \texttt{Product}: images without background and \texttt{Real-World}: regular images captured with a camera. The figure displays examples from 16 of the 65 categories.</em>
<br />
<br />

## Data Collection
The images in the dataset were collected using a python web-crawler that crawled through several search engines and online image directories. This initial run searched for around 120 different objects and produced over 100,000 images across the different categories and domains. These images were then filtered to ensure that the desired object was in the picture. Categories were also filtered to make sure that each category had at least a certain number of images. The latest version of the dataset contains around 15,500 images from 65 different categories.

| Domain     | Min: # |Min: Size              |Max: Size              |  Acc.         |
| :--------- |:------:|:-------------------:|:---------------------:|:-------------:|
| Art        | 15     | 117 \\(\times\\) 85 pix.|4384 \\(\times\\) 2686 pix. |44.99 \\(\pm\\) 1.85 |
| Clipart    | 39     | 18 \\(\times\\) 18 pix. |2400 \\(\times\\) 2400 pix. |53.95 \\(\pm\\) 1.45 |
| Product    | 38     | 75 \\(\times\\) 63 pix. |2560 \\(\times\\) 2560 pix. |66.41 \\(\pm\\) 1.18 |
| Real-World | 23     | 88 \\(\times\\) 80 pix. |6500 \\(\times\\) 4900 pix. |59.70 \\(\pm\\) 1.04 |

<em>Statistics for the Office-Home dataset. **Min: #** is the minimum number of images of each object for the specified domain. **Min: Size** and **Max: Size** are the minimum and maximum image sizes in the domain. **Acc:** is the classification accuracy using a linear svm (LIBLINEAR) classifier with 5-fold cross-validation using deep features extracted from the VGG-F deep network.</em>

## Object Categories
The 65 object categories in the dataset are:
```
Alarm Clock, Backpack, Batteries, Bed, Bike, Bottle, Bucket, Calculator, Calendar, Candles,
Chair, Clipboards, Computer, Couch, Curtains, Desk Lamp, Drill, Eraser, Exit Sign, Fan,
File Cabinet, Flipflops, Flowers, Folder, Fork, Glasses, Hammer, Helmet, Kettle, Keyboard,
Knives, Lamp Shade, Laptop, Marker, Monitor, Mop, Mouse, Mug, Notebook, Oven, Pan,
Paper Clip, Pen, Pencil, Postit Notes, Printer, Push Pin, Radio, Refrigerator, ruler,
Scissors, Screwdriver, Shelf, Sink, Sneakers, Soda, Speaker, Spoon, Table, Telephone,
Toothbrush, Toys, Trash Can, TV, Webcam
```

## Fair Use Notice
*(adapted from [Christopher Thomas](http://people.cs.pitt.edu/~chris/photographer/))*
This dataset contains some copyrighted material whose use has not been specifically authorized by the copyright owners. In an effort to advance scientific research, we make this material available for academic research. We believe this constitutes a __fair use__ of any such copyrighted material as provided for in section 107 of the US Copyright Law. In accordance with Title 17 U.S.C. Section 107, the material on this site is distributed without profit to those who have expressed a prior interest in receiving the included information for non-commercial research and educational purposes. For more information on fair use please [click here](https://www.law.cornell.edu/uscode/text/17/107 "Fair Use Notice"). If you wish to use copyrighted material on this site or in our dataset for purposes of your own that go beyond non-commercial research and academic purposes, you must obtain permission directly from the copyright owner.
