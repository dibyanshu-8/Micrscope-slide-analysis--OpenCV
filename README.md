# Microscope Slide Analysis Tool

An automated digital pathology tool built with Python and OpenCV to analyze H&E stained microscope slide images. This project, designed for a Jupyter/Colab environment, provides automated cell nuclei counting and image focus quality assessment.


##  Project Overview

This tool serves as a proof-of-concept for automating key tasks in histopathology. Manually analyzing microscope slides is time-consuming and subjective. This script provides an objective, rapid analysis of two key metrics: the number of cell nuclei (a proxy for cell density) and the sharpness of the image (a critical quality control metric for digital slide scanners).

##  Key Features

* **Automated Nuclei Counting:** Uses color segmentation in the HSV color space to accurately detect and count cell nuclei stained by Hematoxylin.
* **Focus Quality Assessment:** Implements the Laplacian variance method to calculate a "focus score," objectively determining if an image is sharp or blurry.
* **Self-Contained & Reproducible:** The script downloads its own sample H&E image, making it easy to run and test for anyone, anywhere.
* **Visual Feedback:** Uses Matplotlib to display the stages of the analysis, from the original image to the final output with detected nuclei highlighted.

##  Technology Stack

* **Language:** Python 3
* **Core Libraries:**
    * `OpenCV` - For all computer vision tasks (image manipulation, color space conversion, contour detection).
    * `NumPy` - For numerical operations and array manipulation.
    * `Matplotlib` - For visualizing the images and results.
    * `Requests` - For downloading the sample image.
* **Environment:** Google Colab or Jupyter Notebook

##  How It Works

The analysis is performed in two main pipelines:

### 1. Nuclei Counting Pipeline

1.  **Load Image:** A sample H&E stained image is downloaded from the web.
2.  **Color Space Conversion:** The image is converted from the standard BGR format to **HSV (Hue, Saturation, Value)**, which is more effective for isolating specific colors.
3.  **Color Masking:** A mask is created to isolate only the pixels that fall within the specific color range of the purple/blue Hematoxylin stain used on cell nuclei.
4.  **Contour Detection:** `cv2.findContours` is used on the mask to find the outlines of all detected nuclei.
5.  **Filtering & Counting:** The contours are filtered by area to remove small noise, and the remaining contours are counted to get the final cell count.

### 2. Focus Analysis Pipeline

1.  **Grayscale Conversion:** The image is converted to grayscale, as focus is dependent on edges and not color.
2.  **Laplacian Operator:** A Laplacian filter is applied to the grayscale image. This filter highlights regions of high-frequency change (i.e., sharp edges).
3.  **Variance Calculation:** The variance of the Laplacian-filtered image is calculated. A high variance indicates the presence of many sharp edges, meaning the image is **in focus**. A low variance indicates a lack of sharp edges, meaning the image is **blurry**.

---

