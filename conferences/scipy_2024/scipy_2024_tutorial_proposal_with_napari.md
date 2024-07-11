# SciPy 2024 tutorial proposal: joint proposal with scikit-image and napari

## Title: image analysis and visualization in Python with scikit-image, napari, and friends

## Abstract (100 words)

Between telescopes and satellite cameras and MRI machines and microscopes, scientists are producing more images than they can realistically look at. They need specialized viewers for multi-dimensional images, and automated tools to help process those images into knowledge. In this tutorial, we will cover the fundamentals of algorithmic image analysis, starting with how to think of images as NumPy arrays, moving on to basic image filtering, and finishing with a complete workflow: segmenting a 3D image into regions and making measurements on those regions. At every step, we will visualize and understand our work using matplotlib and napari.

## Description (500 words)

Between telescopes and satellite cameras and MRI machines and microscopes, scientists are producing more images than they can realistically look at. They need specialized viewers for multi-dimensional images, and automated tools to help process those images into knowledge.

This tutorial is aimed at folks who have some experience in scientific computing with Python, but are new to image analysis. To get the most out of it, they should have done some work with NumPy arrays — no need to be an expert! — but they don't need to know [an image from a pipe](https://en.wikipedia.org/wiki/The_Treachery_of_Images). We will cover the fundamentals of working with images in scientific Python. The tutorial will be split into four parts, of about 45 minutes each, plus breaks:

- **Images are just NumPy arrays.** In this section we will cover the basics: how to think of images not as things we can see but numbers we can analyze.
- **Changing the structure of images with image filtering.** In this section we will define *filtering*, a fundamental operation on signals (1D), images (2D), and higher-dimensional images (3D+). We will use filtering to find various structures in images, such as *blobs* and *edges*. Putting NumPy, SciPy, scikit-image, and scikit-learn together, we'll show how these fundamental filters are related to modern convolutional neural networks.
- **Finding regions in images and measuring their properties.** In this section we will define image segmentation — splitting up images into regions. We will show how segmentation is commonly represented in the scientific Python ecosystem, some basic and advanced methods to do it, and use it to take measurements of segmented objects in our images. We will use scikit-image for some basics, and to make object measurements, but we'll also demonstrate how to use a modern, neural-network-based library to find our imaged objects quickly and get on with our science: measuring the things we've imaged.
- **Q&A/Quick tour of advanced features.** This section will be more freestyle and will depend on the audience. We may do a guided tour of other advanced image analysis topics, answer lingering questions about the previous sections, or walk around the room and help people apply what they've learned to their own data of interest.

Attendees will leave understanding how to work with images in Python, knowing some of the main libraries that can help them do that, and knowing where to get more help if they need it.

## Notes for the organiser

## Image

![](https://i.imgur.com/Az2JDJR.jpg)

## Speakers

Juan Nunez-Iglesias
Lars Grüter
Kira Evans

## Outline

- Introduction/Images are NumPy arrays (40 min) ([preliminary example notebook](https://github.com/jni/lma-2021-bioimage-analysis-python/blob/main/lectures/0_images_are_arrays.ipynb))
- break (15 min)
- Image filtering (55 min) ([preliminary example notebook](https://github.com/jni/lma-2021-bioimage-analysis-python/blob/main/lectures/1_image_filters.ipynb))
- break (20 min)
- Segmentation and region properties (50 min) ([preliminary example notebook](https://github.com/jni/lma-2021-bioimage-analysis-python/blob/main/lectures/2_segmentation_and_regionprops.ipynb))
- break (15 min)
- Q&A/advanced topics (40 min)

Total: 4h.

Each notebook contains some prefilled code but also numerous exercises that will be done by attendees in class.

## Additional information

This tutorial is based on a long history of well-received scikit-image tutorials at SciPy, EuroSciPy, and other venues (see for example [2018 pt 1](https://youtu.be/arXiv-TM7DY), [2018 pt 2](https://youtu.be/pZATswy_IsQ), [2019](https://youtu.be/d1CIV9irQAY)), and a shorter history of napari tutorials (e.g. [SciPy 2022](https://youtu.be/vismuuc4y1I)). This year, we hope to continue to improve the tutorial with the most relevant material for current audiences. For example, we will quickly cover a classical segmentation algorithm, before demonstrating how to "plug in" modern, deep-learning-based algorithms into our scientific measurement workflows. We will also use the napari n-dimensional viewer as our main viewer, allowing us to demonstrate image analysis for more complex images than before.

## Prerequisites

Attendees should have *basic* knowledge of:
- Python (imports, if clauses, list indexing, for loops, function definition and return statements)
- Python environments — they should be able to make a new Python environment for the tutorial
- Jupyter notebooks: they should know how to launch a Jupyter notebook, enter code in cells, and execute the code
- NumPy arrays and simple array arithmetic

## Prior programming level of knowledge expected

- Intermediate (see above)
