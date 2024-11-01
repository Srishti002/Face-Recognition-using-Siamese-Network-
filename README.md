# Face Recognition using Siamese Neural Network
## Introduction
This project is about face recognition using a Siamese Neural Network. 
- Traditionally Siamese networks are using pairs of training samples such as anchor-positive and anchor-negative pairs. So this is kind a supervised type where we have labels anchor-positive as 1 and anchor-negative as 0.
- But we can also use unsupervised approach here as positive training data are chosen within one dataset  based on their similarity score using cosine similarity with the anchor and negative training data are selected using the same criterion but from the separate dataset.
- But in this project we will follow supervised approach.

## Siamese Neural Network :
![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-27%20203139.png)

A siamese neural network consists of twin networks which accept distinct inputs but are joined by an energy function at the top.
For example we have anchor-postive/negative pair then these these two images will separately go in given hidden layers. After this we will compute L1 distance between these two feature vectors and then pass through our classifier which will classify 0 or 1. 

## Step By Step Guide :

### 1. Dataloading and Pre-processing:-
- collected real time positive and anchor images of myself using OpenCv function. Collected atmost 300-400 images of myself separately for anchor and positive and also saved them in their respective positive and anchor directories.
- For negative images , I used LFW(labelled faces in wild) dataset. Link : https://www.kaggle.com/datasets/jessicali9530/lfw-dataset 
- Then we save all negative images in a separate folder.
- Then we make dataset of 180 images from each folder of anchor,positive,negative.
  ![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-27%20222724.png)

- Then we have to also apply transformation as :
  
  ![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-27%20223011.png)

- Now we have to get our final data with proper labels assigned. So first we will make dataset with '1' label with anchor-postive pairs and then '0' label with anchor-negative pairs. After this we will concatenate both datasets to get final dataset containing both anchor-postive and anchor-negative pairs with their respective labels.
  
  ![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-27%20223700.png)

- Dividing into training and testing set :

  ![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-27%20224500.png)

### 2. Model :
![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-27%20224833.png)

- First we will make embedding layer through which each of anchor and positive/negative images will be passed and we will get feature vector of both .

  ![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-27%20225949.png)

- Then we will make distance layer calculating L1 distance :

  ![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-27%20230905.png)

- Now final we will add a classifier and add both above functions under one single function as :
  
  ![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-27%20231848.png)

### 3. Training :
For training purpose :

> Epochs = 30

> Loss : Binary Cross Entropy Loss

> Optimizer : Adam Optimizer

  Training Loss  :
  
  ![](https://github.com/Srishti002/Face-Recognition-using-Siamese-Network-/blob/main/Screenshot%202024-10-28%20021018.png)

### 4. Real time testing :
- In this we will create one directory in which we will save our real time captured pic which is done through opencv functions and one more directory in which we will have some positive images means if we want to detect our face then this positive directory contains pics of ourselves as by this we will compare our real time captured pic with these positive images . we will *'True'* when the model detects the same face and *'wrong'* when it detects different face
  

