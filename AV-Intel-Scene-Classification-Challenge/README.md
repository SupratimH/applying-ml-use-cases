# Intel Scene Classification Challenge
* Competition link: https://datahack.analyticsvidhya.com/contest/practice-problem-intel-scene-classification-challe/
* Dataset link: https://datahack.analyticsvidhya.com/contest/practice-problem-intel-scene-classification-challe/#data_dictionary

## Problem Statement
How do we, humans, recognize a forest as a forest or a mountain as a mountain? We are very good at categorizing scenes based on the semantic representation and object affinity, but we know very little about the processing and encoding of natural scene categories in the human brain. In this problem, you are provided with a dataset of ~25k images from a wide range of natural scenes from all around the world. Your task is to identify which kind of scene can the image be categorized into.

<img src="https://media.mnn.com/assets/images/2016/08/Jaymi-Heimbuch-_JHX6011-01.jpg.653x0_q80_crop-smart.jpg" width="400px" height="200px"/>

## Data Description
- There are 17034 images in train and 7301 images in test data. The categories of scenes and their corresponding labels in the dataset are as follows -
```
'buildings' -> 0
'forest' -> 1
'glacier' -> 2
'mountain' -> 3
'sea' -> 4
'street' -> 5
```
- There are three files provided, viz train.zip, test.csv and sample_submission.csv which have the following structure.

| Variable	| Definition |
| ------------- | ----------------- |
| image_name	| Name of the image in the dataset (ID column) |
| label | Category of natural scene (target column) |
- train.zip contains the images corresponding to both train and test set along with the true labels for train set images in train.csv

## Objective
Create a classifier capable of predicting which of the above scenaries is present in an image.

## Evaluaton Metric
Submissions are evaluated on Accuracy between the predicted probability and the observed target.

## Solution Approach
- GPU is needed to train the implemented algorithms, so I used Google Colab platform for development.
- All images are resized to 150x150 pixels, hence no further resizing was required.
- I used `tensorflow.keras.preprocessing.image.ImageDataGenerator` to generate augmented images, techniques used - rotation, width shift, height shift, shear, zoom and horizontal flip.
- 20% of training data was reserved for cross-validation.
- I decided to try some popular CNN architectures like VGG and ResNet, with pre-trained weights on imagenet dataset.
- VGG-19 based model was used as baseline. Accuracy on CV set using **VGG-19** based architecture and pre-trained weights hovered around ~85%.
- Using **ResNet50** increased the accuracy on CV set to ~94%.
- The nature of this problem is closer to `Places365` problem, rather than `Imagement` problem. So it can be expected that models trained on Places365 dataset will give a better result.
- There are few pre-trained models on [Places365](https://github.com/CSAILVision/places365) dataset available as well. But most of those are built of Caffe and PyTorch. Since I used Tensorflow and Keras for this implementation, I was not able to use those as-is.
- However, [GKalliatakis](https://github.com/GKalliatakis) has done an wonderful job in training a VGG-19 network on Places365 dataset. It is available in [this repository](https://github.com/GKalliatakis/Keras-Application-Zoo). I downloaded the weights without top FC layers and tried on this problem, unfortunately the score did not improve much.
- Maybe a ResNet model trained on Places365 would give a better result, but currently it is not available on Keras.
- I tried few more architectures like DenseNet, InceptionResnet etc, but none of those resulted in improved score.
- At the end I decided to go with ResNet50 based model as final submission.
- **Problem:** Training the algos was very time and resource consuming, and Google Colab often used to time-out. This was a major bottleneck in training. I saved the weights every few epochs to get around this problem.
- :white_check_mark: Final submitted code: [scene-classification-final-code.ipynb](scene-classification-final-code.ipynb)

## Results and Observations from predictions on CV set using ResNet50 model
- **Confusion Matrix**

![confusion_matrix](https://github.com/SupratimH/applying-ml-use-cases/blob/master/AV-Intel-Scene-Classification-Challenge/images/conf_matrix_resnet50.png) 
- **Scores**

![score](https://github.com/SupratimH/applying-ml-use-cases/blob/master/AV-Intel-Scene-Classification-Challenge/images/score_resnet50.PNG)
- **Train accuracy was ~97% and CV accuracy was ~93%**
- As can be seen from the confusion matrix and scores, the model is able to detect `forest` and `sea` very accurately.
- The model is confused between `buildings` and `streets`, and `glaciers` and `mountains`. A closer look at few randomly selected images from training directory reveals that these combination indeed look similar, because in most images both the scene are present (eg - building and street are present together, mountains and glaciers are present together). In addition, snow-clad mountains and glaciers look very similar, thus confusing the model.
- If the above classification problem can be solved, the accuracy will improve to almost near-perfection.
- :point_right: **Score on test data - Public LB: 0.9456621005 and Private LB: 0.9330855019**

## Instruction to run this code
- Requirements: Python 3, Numpy, Matplotlib, Tensorflow and Keras
- Download the dataset from link provided above
- Follow the exact directory structure as provided in this repo
- Set the `home_dir` variable in code to abolute path where this repo is copied to, or to `'.'`
- `scene-classification-final-code.ipynb` is the final cleaned up code. Names of each of the other source code file is descriptive enough suggesting the architecture implemented
- All additional information/instructions are provided in respective notebooks

## Contact
:love_letter: For any feedback or questions or just to say "Hi", drop me a line anytime at supratimh[at]gmail[dot]com.

Thank you for reading :heart:
