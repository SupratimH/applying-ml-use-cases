# DeepArtist : Identify Artist from Paintings

## "I dream of painting and then I paint my dream." - Vincent Van Gogh
<p align="center"><img src="https://media.giphy.com/media/WLCACa0Onhbhe/giphy.gif" width="400px" height="200px"/></p>

## Introduction
Creation of art is among the highest form of expression of human mind and imagination. The ability of communicating imagination sets us apart from all other beings. Painting, being an expression of visual language, have attracted and connected the brilliant human minds since the dawn of civilization - from early drawings on walls of caves to paper or glass paintings of modern times, from charcoals in prehistoric times to water, oil, or pastel colors of today. We have travelled a long way, and have finally reached a stage where not only humans but computers, another brilliant creation of human minds, is creating paintings.

For an enthusiast of arts, identifying the paintings of her favorite artists is not that difficult, given years of careful practice and research. Given a painting, she can easily identify if it was painted by a painter she is passionate about. But can a computer do the same? Can a machine without emotions identify who the genius is behind a mindblowing painting?

In this kernel, let us try to explore that direction, using techniques of deep learning.

## Objective: 
Develop an algorithm which will identify the artist when provided with a painting, with state of the art precision.

## Data Source
Collection of artworks of the 50 most influential artists of all time, scraped from artchallenge.ru during the end of February 2019. Special thanks to [Icaro](https://www.kaggle.com/ikarus777) for sharing this wonderful dataset! It can be downloaded from [Kaggle dataset section](https://www.kaggle.com/ikarus777/best-artworks-of-all-time).

## High-level approach to solution:
### Data processing:
* There are paintings of 50 artists in the dataset. However only 11 artists have more than 200 paintings available here.
* To reduce computation and better training, I decided to use the paintings of these 11 artists only.
* Since this is an imbalanced datset (Van Gogh has 877 paintings whereas Marc Chagall has only 239), `class_weight` is important. Infact, it improved model performance substantially.
* I used Keras `ImageDataGenerator` for data augmentation. This is not a traditional object detection problem, hence the augmentation approch should be used very carefully.
* I couldn't experiment in detail, but so far `zoom_range` worked well. 

### Modelling and Training:
* Use convolutional neural network based approach, with a pre-defined architecture as baseline.
* I tried multiple architectures, however `ResNet50` worked well so far.
* Pretrained weights on `imagenet` with transfer learning helped the model train better.
* The objective is to identify artist and not objects in the images. So the model should understand the style of the image better rather than the final output. Hence, training of shallow layers is more important than the deeper layers.
* The above statement is based on my understanding of the problem and experiments and observations.
* Training the model for more iterations might improve the performance, at the cost of computation resource and longer training time.

### Predictions:
* <b>The final model could identify the artists with an approximate accuracy of 99% on training set and 87% on cross-validation set.</b>

## Instruction to run this code
- Requirements: Python 3, Numpy, Matplotlib, Tensorflow and Keras
- Download the dataset from link provided above
- Modify the input file paths and point to your local directory where data the downloaded data is stored
- If using Kaggle to run these notebooks, then just upload a notebook in a kernel (for the dataset linked above) and it'll work fine without any modification.  

## Web Application
* The model is deployed as a web-application on Heroku cloud - https://find-artist.herokuapp.com/
* Code of the web application is available here - https://github.com/SupratimH/deepartist-web-application

## Contact
:love_letter: For any feedback or questions or just to say "Hi", drop me a line anytime at supratimh[at]gmail[dot]com.

To read about other projects I am working on, please visit [my home page](https://supratimh.github.io).

Thank you for reading :heart:
