## Requirement

### To update the MNIST colab notebook so that it achieves the following -
1. 99.4 accuracy 
2. Uses less than 20k parameters 
3. Achieves the accuracy in less than 20 epochs.

## Approach

### Part -1

The network class updated to reduce the number of channels because use of excessive number of channels leads to wrong patterns/objects formation when combined. The images in the dataset are handwritten digits from 0 to 9 and of size 28x28x1. Hence, the number of channels cannot be exorbitantly large. Excessive increase in channels/features unnecessarily breaks down the images into extremely small parts (which eventually would belong to majority of the digits) and hence chances of a predicting a wrong digit increase. The number of channels were limited to 32. This also in turn reduced the number of parameters.

The network has the following structure- 

<pre>

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1            [-1, 3, 28, 28]              30
            Conv2d-2            [-1, 6, 28, 28]             168
         MaxPool2d-3            [-1, 6, 14, 14]               0
            Conv2d-4           [-1, 12, 14, 14]             660
            Conv2d-5           [-1, 24, 14, 14]           2,616
         MaxPool2d-6             [-1, 24, 7, 7]               0
            Conv2d-7             [-1, 32, 5, 5]           6,944
            Conv2d-8             [-1, 12, 3, 3]           3,468
            Conv2d-9             [-1, 10, 1, 1]           1,090
================================================================

</pre>
Total params: 14,976


### Part -2
The initial batch size was set to 128. This was varied by increasing it to 512, 1024 and reducing it to 64,32.
The ideal batch size turned out to be 64 in this case. Any further increase or decrease lead to loss of accuracy.

### Part -3
The function to test the model was updated so that it returned the accuracy. This was later used to adjust the learning rate.

### Part -4
The learning rate was adjusted using the below rules - 
Initial learning rate = .02
- If accuracy is < 90% then keep on increasing learning rate by a factor of 2 till a maximum value of 0.1.
- If the accuracy is in the range of 90% and 99% fix the learning rate to 0.02
- If the accuracy reaches 99% reduce the learning rate by a factor of 2 with a minimum limit set to .0001.

After every epoch once the learning rate was adjusted the optimizer was re-initialized with the new learning rate.

optimizer = optim.SGD(model.parameters(), lr=learning_rate, momentum=0.9)



