# Session - 6 Assignment

## Requirement

To create 3 versions of models with the best network developed so far.

- Version 1 Model with Batch Normalization and L1 Regularization
- Version 2 Model with Layer Normalization
- Version 3 Model with Group Normalization 

## Approach

The network class was modified to accept a parameter that would decide the type of normalization to be used.
Parameter values as below:
B - For BN + L1 Regularization
L - For Layer Normalization
G - For group Normalization (Group of 4 per layer has been used for this assignment)

The Network class has been saved in a different file named as model.py
A Notebook file was created to create 3 versions of the model.
Model parameteres and output as below.


## Model Summary

### Version -1 (Model with BN + L1)
<pre>
The model parameters for Batch Mormalization

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1            [-1, 8, 26, 26]              72
       BatchNorm2d-2            [-1, 8, 26, 26]              16
              ReLU-3            [-1, 8, 26, 26]               0
            Conv2d-4            [-1, 8, 24, 24]             576
       BatchNorm2d-5            [-1, 8, 24, 24]              16
              ReLU-6            [-1, 8, 24, 24]               0
            Conv2d-7            [-1, 8, 22, 22]             576
       BatchNorm2d-8            [-1, 8, 22, 22]              16
           Dropout-9            [-1, 8, 22, 22]               0
             ReLU-10            [-1, 8, 22, 22]               0
        MaxPool2d-11            [-1, 8, 11, 11]               0
           Conv2d-12             [-1, 16, 9, 9]           1,152
      BatchNorm2d-13             [-1, 16, 9, 9]              32
          Dropout-14             [-1, 16, 9, 9]               0
             ReLU-15             [-1, 16, 9, 9]               0
           Conv2d-16             [-1, 16, 7, 7]           2,304
      BatchNorm2d-17             [-1, 16, 7, 7]              32
          Dropout-18             [-1, 16, 7, 7]               0
             ReLU-19             [-1, 16, 7, 7]               0
           Conv2d-20              [-1, 8, 7, 7]             128
      BatchNorm2d-21              [-1, 8, 7, 7]              16
          Dropout-22              [-1, 8, 7, 7]               0
             ReLU-23              [-1, 8, 7, 7]               0
           Conv2d-24             [-1, 32, 5, 5]           2,304
      BatchNorm2d-25             [-1, 32, 5, 5]              64
          Dropout-26             [-1, 32, 5, 5]               0
             ReLU-27             [-1, 32, 5, 5]               0
           Conv2d-28             [-1, 16, 5, 5]             512
      BatchNorm2d-29             [-1, 16, 5, 5]              32
          Dropout-30             [-1, 16, 5, 5]               0
             ReLU-31             [-1, 16, 5, 5]               0
        AvgPool2d-32             [-1, 16, 1, 1]               0
           Conv2d-33             [-1, 10, 1, 1]             160
================================================================
Total params: 8,008
Trainable params: 8,008
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.47
Params size (MB): 0.03
Estimated Total Size (MB): 0.50
----------------------------------------------------------------
----------------------------------------------------------------

</pre>

### Version -2 (Model with Layer Normalization)
<pre>
The model parameters for Layer Mormalization

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1            [-1, 8, 26, 26]              72
         LayerNorm-2            [-1, 8, 26, 26]               0
              ReLU-3            [-1, 8, 26, 26]               0
            Conv2d-4            [-1, 8, 24, 24]             576
         LayerNorm-5            [-1, 8, 24, 24]               0
              ReLU-6            [-1, 8, 24, 24]               0
            Conv2d-7            [-1, 8, 22, 22]             576
         LayerNorm-8            [-1, 8, 22, 22]               0
           Dropout-9            [-1, 8, 22, 22]               0
             ReLU-10            [-1, 8, 22, 22]               0
        MaxPool2d-11            [-1, 8, 11, 11]               0
           Conv2d-12             [-1, 16, 9, 9]           1,152
        LayerNorm-13             [-1, 16, 9, 9]               0
          Dropout-14             [-1, 16, 9, 9]               0
             ReLU-15             [-1, 16, 9, 9]               0
           Conv2d-16             [-1, 16, 7, 7]           2,304
        LayerNorm-17             [-1, 16, 7, 7]               0
          Dropout-18             [-1, 16, 7, 7]               0
             ReLU-19             [-1, 16, 7, 7]               0
           Conv2d-20              [-1, 8, 7, 7]             128
        LayerNorm-21              [-1, 8, 7, 7]               0
          Dropout-22              [-1, 8, 7, 7]               0
             ReLU-23              [-1, 8, 7, 7]               0
           Conv2d-24             [-1, 32, 5, 5]           2,304
        LayerNorm-25             [-1, 32, 5, 5]               0
          Dropout-26             [-1, 32, 5, 5]               0
             ReLU-27             [-1, 32, 5, 5]               0
           Conv2d-28             [-1, 16, 5, 5]             512
        LayerNorm-29             [-1, 16, 5, 5]               0
          Dropout-30             [-1, 16, 5, 5]               0
             ReLU-31             [-1, 16, 5, 5]               0
        AvgPool2d-32             [-1, 16, 1, 1]               0
           Conv2d-33             [-1, 10, 1, 1]             160
================================================================
Total params: 7,784
Trainable params: 7,784
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.47
Params size (MB): 0.03
Estimated Total Size (MB): 0.50
----------------------------------------------------------------
----------------------------------------------------------------

</pre>

### Version -3 (Model with Group Normalization)
<pre>
The model parameters for Group Mormalization

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1            [-1, 8, 26, 26]              72
         GroupNorm-2            [-1, 8, 26, 26]              16
              ReLU-3            [-1, 8, 26, 26]               0
            Conv2d-4            [-1, 8, 24, 24]             576
         GroupNorm-5            [-1, 8, 24, 24]              16
              ReLU-6            [-1, 8, 24, 24]               0
            Conv2d-7            [-1, 8, 22, 22]             576
         GroupNorm-8            [-1, 8, 22, 22]              16
              ReLU-9            [-1, 8, 22, 22]               0
        MaxPool2d-10            [-1, 8, 11, 11]               0
           Conv2d-11             [-1, 16, 9, 9]           1,152
        GroupNorm-12             [-1, 16, 9, 9]              32
          Dropout-13             [-1, 16, 9, 9]               0
             ReLU-14             [-1, 16, 9, 9]               0
           Conv2d-15             [-1, 16, 7, 7]           2,304
        GroupNorm-16             [-1, 16, 7, 7]              32
          Dropout-17             [-1, 16, 7, 7]               0
             ReLU-18             [-1, 16, 7, 7]               0
           Conv2d-19              [-1, 8, 7, 7]             128
        GroupNorm-20              [-1, 8, 7, 7]              16
          Dropout-21              [-1, 8, 7, 7]               0
             ReLU-22              [-1, 8, 7, 7]               0
           Conv2d-23             [-1, 32, 5, 5]           2,304
        GroupNorm-24             [-1, 32, 5, 5]              64
          Dropout-25             [-1, 32, 5, 5]               0
             ReLU-26             [-1, 32, 5, 5]               0
           Conv2d-27             [-1, 16, 5, 5]             512
        GroupNorm-28             [-1, 16, 5, 5]              32
          Dropout-29             [-1, 16, 5, 5]               0
             ReLU-30             [-1, 16, 5, 5]               0
        AvgPool2d-31             [-1, 16, 1, 1]               0
           Conv2d-32             [-1, 10, 1, 1]             160
================================================================
Total params: 8,008
Trainable params: 8,008
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.44
Params size (MB): 0.03
Estimated Total Size (MB): 0.47
----------------------------------------------------------------

</pre>

## Model Rseults

### Test/Validation Loss for all 3 models together

