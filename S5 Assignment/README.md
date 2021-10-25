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
1.	The base version of the network has been cleaned
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
2.	Continued basic transformations done to the original dataset like converting to tensor and normalizing.

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
1.	Adjust the network by shifting the Maxpool layer after 2 convolutions.
2.	Reduce Parameters.
3.	Introduce stepped reduction of learning rate.

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
1.	Overfitting is eliminated. In fact we see some underfitting.
2.	Accuracy needs improvement. Accuracy is almost same as compared to Step -2.

