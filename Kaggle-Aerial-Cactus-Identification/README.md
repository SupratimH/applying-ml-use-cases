# Aerial Cactus Identification
* Competition link: https://www.kaggle.com/c/aerial-cactus-identification/overview
* Dataset link: https://www.kaggle.com/c/aerial-cactus-identification/data

## Problem Statement
To assess the impact of climate change on Earth's flora and fauna, it is vital to quantify how human activities such as logging, mining, and agriculture are impacting our protected natural areas. Researchers in Mexico have created the VIGIA project, which aims to build a system for autonomous surveillance of protected areas. A first step in such an effort is the ability to recognize the vegetation inside the protected areas. In this competition, you are tasked with creation of an algorithm that can identify a specific type of cactus in aerial imagery.

<img src="https://cdn.britannica.com/40/193840-131-258B734E.jpg" width="400px" height="200px"/>

## Data Description
This dataset contains a large number of 32 x 32 thumbnail images containing aerial photos of a columnar cactus (Neobuxbaumia tetetzo). Kaggle has resized the images from the original dataset to make them uniform in size. The file name of an image corresponds to its id.

## Objective
Create a classifier capable of predicting whether an image contains a columnar cactus.

## Evaluaton Metric
Submissions are evaluated on area under the ROC curve between the predicted probability and the observed target.

## Solution Approach
- This is a typical binary classification problem for images. Since the images are resized to 32x32 pixels, it is very difficult to visually figure out the difference between images which has cactus and those which does not, due to the small size.
- 20% of training data was reserved for cross-validation.
- I decided to try some popular CNN architectures like VGG and ResNet, with and without pre-trained weights.
- The VGG-16 based network gave best result on Kaggle test data. I used pre-trained weights on imagenet for transfer learning (on Keras), and then finetuned all the layers. **The AUC score on Kaggle public LB is 0.9963.**
- I tried by building a simple CNN network but the AUC on CV set was slightly less.
- Here's a bit more detail on the approaches (all implementations are done with Tensorflow and Keras):
#### [Approach 1](cactus-identification-cnn-and-transfer-learning.ipynb):
- Used a VGG19 architecture without the top FC layers.
- Did not use the pre-trained weights, so trained all layers with the available dataset. Aldo, did not create augmented data.
- Precision, Recall and F1-score on CV set is 1, and AUC is 0.9984.
#### [Approach 2](cactus-identification-cnn-data-aug-vgg19.ipynb):
- Used a VGG19 architecture without the top FC layers, but used pre-trained weights.
- Did data augmentation using `ImageDataGenerator` class of `Keras`.
- The best AUC on CV set is 0.9953.
#### [Approach 3](cactus-identification-cnn-data-aug-vgg16.ipynb):
- Used a VGG16 architecture without the top FC layers, but used pre-trained weights.
- Did data augmentation using `ImageDataGenerator` class of `Keras`.
- The best AUC on CV set is 0.9968.

## Instruction to run this code
- Requirements: Python 3, Numpy, Matplotlib, Tensorflow and Keras
- Download the dataset from link provided above
- Modify the `input file path` and point to your local directory where data the downloaded data is stored
- If using Kaggle to run these notebooks, then just upload a notebook in a kernel (for this competition) and it'll work fine without any modification.  

## Contact
:love_letter: For any feedback or questions or just to say "Hi", drop me a line anytime at supratimh[at]gmail[dot]com.

Thank you for reading :heart:
