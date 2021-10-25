# Session - 5 Assignment

## Data Overview


MNIST ("Modified National Institute of Standards and Technology") dataset of computer vision. The MNIST database contains 60,000 training images and 10,000 testing images. Half of the training set and half of the test set were taken from NIST's training dataset, while the other half of the training set and the other half of the test set were taken from NIST's testing dataset.This project implements a beginner classification task on MNIST dataset with a Convolutional Neural Network(CNN) model.

![image](https://user-images.githubusercontent.com/70502759/137764343-c1134fa1-94d2-40b0-bf21-dcd78b3ed4e1.png)
  
  This project will automatically dowload and process the MNIST dataset
  
  Design the model architecture for MNIST with following constraint :
    
    99.4% validation accuracy
    Less than 10k Parameters
    Less than 15 Epochs
    
## Approach

Our approach would be to update the model and based on Train/test results necessary changes would be done. This has been achieved over 5 steps. Details of each step is as below:

## Step - 1

Changes done: 
1.	The base version of the network was cleaned
2.	Parameters reduced from 6,379,786 to 13,312
3.	Only basic transformations done to the original dataset like converting to tensor and normalizing

Base Model parameters:
<pre>

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1           [-1, 32, 28, 28]             320
            Conv2d-2           [-1, 64, 28, 28]          18,496
         MaxPool2d-3           [-1, 64, 14, 14]               0
            Conv2d-4          [-1, 128, 14, 14]          73,856
            Conv2d-5          [-1, 256, 14, 14]         295,168
         MaxPool2d-6            [-1, 256, 7, 7]               0
            Conv2d-7            [-1, 512, 5, 5]       1,180,160
            Conv2d-8           [-1, 1024, 3, 3]       4,719,616
            Conv2d-9             [-1, 10, 1, 1]          92,170
================================================================
Total params: 6,379,786
Trainable params: 6,379,786
Non-trainable params: 0
----------------------------------------------------------------

</pre>

Updated Model parameters:
<pre>

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1           [-1, 12, 26, 26]             108
              ReLU-2           [-1, 12, 26, 26]               0
            Conv2d-3           [-1, 12, 24, 24]           1,296
              ReLU-4           [-1, 12, 24, 24]               0
            Conv2d-5           [-1, 24, 22, 22]           2,592
              ReLU-6           [-1, 24, 22, 22]               0
         MaxPool2d-7           [-1, 24, 11, 11]               0
            Conv2d-8           [-1, 12, 11, 11]             288
              ReLU-9           [-1, 12, 11, 11]               0
           Conv2d-10             [-1, 12, 9, 9]           1,296
             ReLU-11             [-1, 12, 9, 9]               0
           Conv2d-12             [-1, 24, 7, 7]           2,592
             ReLU-13             [-1, 24, 7, 7]               0
           Conv2d-14             [-1, 10, 7, 7]             240
             ReLU-15             [-1, 10, 7, 7]               0
           Conv2d-16             [-1, 10, 1, 1]           4,900
================================================================
Total params: 13,312
Trainable params: 13,312
Non-trainable params: 0
----------------------------------------------------------------

</pre>

Results:
1.	Parameters: 13,312
2.	Best Train Accuracy: 99.06
3.	Best Test Accuracy: 98.70

Inference:
1.	The model is still large but working. 
2.	We see some over-fitting


## Step - 2

Changes done: 
1.	Reduced parameters by introducing GAP layer.
2.	Continued with basic transformations done to the original dataset like converting to tensor and normalizing.

Model parameters

<pre>

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1           [-1, 12, 26, 26]             108
              ReLU-2           [-1, 12, 26, 26]               0
            Conv2d-3           [-1, 12, 24, 24]           1,296
              ReLU-4           [-1, 12, 24, 24]               0
            Conv2d-5           [-1, 24, 22, 22]           2,592
              ReLU-6           [-1, 24, 22, 22]               0
         MaxPool2d-7           [-1, 24, 11, 11]               0
            Conv2d-8           [-1, 12, 11, 11]             288
              ReLU-9           [-1, 12, 11, 11]               0
           Conv2d-10             [-1, 12, 9, 9]           1,296
             ReLU-11             [-1, 12, 9, 9]               0
           Conv2d-12             [-1, 24, 7, 7]           2,592
             ReLU-13             [-1, 24, 7, 7]               0
           Conv2d-14             [-1, 10, 7, 7]             240
             ReLU-15             [-1, 10, 7, 7]               0
        AvgPool2d-16             [-1, 10, 1, 1]               0
================================================================
Total params: 8,412
Trainable params: 8,412
Non-trainable params: 0
----------------------------------------------------------------

</pre>

Results:
1.	Parameters: 8412
2.	Best Train Accuracy: 97.32
3.	Best Test Accuracy: 97.53

Inference:
1.	Overfitting is eliminated. In fact we see some underfitting.
2.	Accuracy needs improvement. Accuracy has decreased as compared to Step -1.
3.	From the training loss curve we see that reducing the learning rate might improve the training accuracy.

## Step - 3

Changes done: 
1.	Adjusted the network by shifting the Maxpool layer after 2 convolutions.
2.	Reduced Parameters.
3.	Introduced stepped reduction of learning rate.

Model parameters

<pre>

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1           [-1, 12, 26, 26]             108
              ReLU-2           [-1, 12, 26, 26]               0
            Conv2d-3           [-1, 24, 24, 24]           2,592
              ReLU-4           [-1, 24, 24, 24]               0
            Conv2d-5           [-1, 12, 24, 24]             288
              ReLU-6           [-1, 12, 24, 24]               0
         MaxPool2d-7           [-1, 12, 12, 12]               0
            Conv2d-8           [-1, 12, 10, 10]           1,296
              ReLU-9           [-1, 12, 10, 10]               0
           Conv2d-10             [-1, 24, 8, 8]           2,592
             ReLU-11             [-1, 24, 8, 8]               0
           Conv2d-12             [-1, 10, 8, 8]             240
             ReLU-13             [-1, 10, 8, 8]               0
           Conv2d-14             [-1, 10, 8, 8]             100
             ReLU-15             [-1, 10, 8, 8]               0
        AvgPool2d-16             [-1, 10, 1, 1]               0
================================================================
Total params: 7,216
Trainable params: 7,216
Non-trainable params: 0
----------------------------------------------------------------

</pre>

Results:
1.	Parameters: 7216
2.	Best Train Accuracy: 97.64
3.	Best Test Accuracy: 97.53

Inference:

1.	Further reduction of model parameters is not helping.
2.	Overfitting is eliminated. In fact we see some underfitting.
3.	Accuracy needs improvement. Accuracy is almost same as compared to Step -2.

## Step - 4

Changes done: 
1.	Introduced regularization methods like dropout and batch normalization.
2.	Continued with basic transformations done to the original dataset like converting to tensor and normalizing.

Model parameters

<pre>

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1           [-1, 12, 26, 26]             108
              ReLU-2           [-1, 12, 26, 26]               0
       BatchNorm2d-3           [-1, 12, 26, 26]              24
           Dropout-4           [-1, 12, 26, 26]               0
            Conv2d-5           [-1, 24, 24, 24]           2,592
              ReLU-6           [-1, 24, 24, 24]               0
       BatchNorm2d-7           [-1, 24, 24, 24]              48
           Dropout-8           [-1, 24, 24, 24]               0
            Conv2d-9           [-1, 12, 24, 24]             288
             ReLU-10           [-1, 12, 24, 24]               0
        MaxPool2d-11           [-1, 12, 12, 12]               0
           Conv2d-12           [-1, 12, 10, 10]           1,296
             ReLU-13           [-1, 12, 10, 10]               0
      BatchNorm2d-14           [-1, 12, 10, 10]              24
          Dropout-15           [-1, 12, 10, 10]               0
           Conv2d-16             [-1, 24, 8, 8]           2,592
             ReLU-17             [-1, 24, 8, 8]               0
      BatchNorm2d-18             [-1, 24, 8, 8]              48
          Dropout-19             [-1, 24, 8, 8]               0
           Conv2d-20             [-1, 10, 8, 8]             240
             ReLU-21             [-1, 10, 8, 8]               0
      BatchNorm2d-22             [-1, 10, 8, 8]              20
          Dropout-23             [-1, 10, 8, 8]               0
           Conv2d-24             [-1, 10, 8, 8]             100
             ReLU-25             [-1, 10, 8, 8]               0
      BatchNorm2d-26             [-1, 10, 8, 8]              20
          Dropout-27             [-1, 10, 8, 8]               0
        AvgPool2d-28             [-1, 10, 1, 1]               0
================================================================
Total params: 7,400
Trainable params: 7,400
Non-trainable params: 0
----------------------------------------------------------------

</pre>

Results:
1.	Parameters: 7400
2.	Best Train Accuracy: 98.2
3.	Best Test Accuracy: 98.7

Inference:
1.	Marginal improvement in accuracy.
2.	Model is underfitting

## Step - 5

Changes done: 
1.	Updated the network to add more parameters
2.	Shifted maxpool layer after 3 convolutions
3.	Introduced Rotational Transformation
4.	Removed Dropout

Model parameters

<pre>

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1            [-1, 8, 26, 26]              72
              ReLU-2            [-1, 8, 26, 26]               0
       BatchNorm2d-3            [-1, 8, 26, 26]              16
            Conv2d-4           [-1, 16, 24, 24]           1,152
              ReLU-5           [-1, 16, 24, 24]               0
       BatchNorm2d-6           [-1, 16, 24, 24]              32
            Conv2d-7           [-1, 32, 22, 22]           4,608
              ReLU-8           [-1, 32, 22, 22]               0
       BatchNorm2d-9           [-1, 32, 22, 22]              64
           Conv2d-10            [-1, 8, 22, 22]             256
             ReLU-11            [-1, 8, 22, 22]               0
        MaxPool2d-12            [-1, 8, 11, 11]               0
           Conv2d-13             [-1, 16, 9, 9]           1,152
             ReLU-14             [-1, 16, 9, 9]               0
      BatchNorm2d-15             [-1, 16, 9, 9]              32
           Conv2d-16             [-1, 32, 7, 7]           4,608
             ReLU-17             [-1, 32, 7, 7]               0
      BatchNorm2d-18             [-1, 32, 7, 7]              64
           Conv2d-19             [-1, 10, 7, 7]             320
             ReLU-20             [-1, 10, 7, 7]               0
      BatchNorm2d-21             [-1, 10, 7, 7]              20
        AvgPool2d-22             [-1, 10, 1, 1]               0
================================================================
Total params: 12,396
Trainable params: 12,396
Non-trainable params: 0
----------------------------------------------------------------

</pre>

Results:
1.	Parameters: 12396
2.	Best Train Accuracy: 99.21
3.	Best Test Accuracy: 99.41

Inference:
1.	The model parameters are slightly more than 10k.
2.	The model shows consistant 99.4% accuracy for last few epochs.
3.	The difference between training and test accuracy is also minimal.
