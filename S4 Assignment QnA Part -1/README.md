

This excel sheet has Neural network calculations which takes in 2 inputs and has a two target outputs. Depending on the value of learning rate with each repetition the loss is minimized. Details of how this has been achieved is explained below. The below image shows the graphical representation of the network.

![](/Images/simple_perceptron_model.jpg)


**The network has the following inputs, outputs and hidden layers.**

*Neurons in input Layer*

i1 = .05

i2 = .1

*Neurons in hidden layer*

h1 = calculated as per weights

a_h1 = sigmoid of h1

h2 = calculated as per weights

a_h2 = sigmoid of h2


*Neurons in output layer*

o1 = calculated as per weights

a_o1 = sigmoid of 01

o2 = calculated as per weights

a_o2 = sigmoid of 02

The weights used are w1, w2, w3, w4 (from input to hidden layer)

The weights used are w5, w6, w7, w8 (from hidden layer to output layer)


*The target values to be achieved are*

t1 = .05

t2 = .99

This network needs to have its weight adjusted so that it can comes as close to the target values as possible.


**Approach**

*Part -1 The below steps show how the output a_o1 and a_o2 is derived.*

h1 = w1*i1 + w2*i2

h2 = w3*i1 + w4*i2

a_h1 = σ(h1) = 1/(1 + exp(-h1))

a_h2 = σ(h2) = 1/(1 + exp(-h2))

o1 = w5*a_h1 + w6*a_h2

o2 = w7*a_h1 + w8*a_h2

a_o1 = σ(o1) = 1/(1 + exp(-o1))

a_o2 = σ(o2) = 1/(1 + exp(-o2))


*Part -2 The below steps how the loss is calculated*

E1 = 1/2*(t1-a_o1)²

E1 = 1/2*(t2-a_o2)²

E_total = E1 + E2

*Part -3 The below steps show how derivative of the error/loss is calculated with respect to the weights for the output layer*

Let us start with weight w5. The path to w5 from E_total is

E1 -> a_o1 -> o1 -> w5

Hence the derivative steps using the chain rule is as below - 

∂E_t/∂w5 = ∂(E1+E2)/∂w5 = E1/∂w5 = (∂E1/∂a_o1)*(∂a_o1/∂o1)*(∂o1/∂w5)

∂E1/∂a_o1 = ∂(1/2*(t1-a_o1)²)/∂a_o1 = 1/2*2(t1-a_o1)*-1 = a_o1 - t1

∂a_o1/∂o1 = a_o1*(1 - a_o1) {Note - Derivative of y where y = σ(x) is x*(1-x)}

∂o1/∂w5 = a_h1

Thus, using the above values we have - 
∂E_t/∂w5 = (a_o1 - t1) * a_o1 * (1 - a_o1) * a_h1

Applying the same principle for w6, w7 and w8 we have - 

∂E_t/∂w6 = (a_o1 - t1) * a_o1 * (1 - a_o1) * a_h2

∂E_t/∂w7 = (a_o2 - t2) * a_o2 * (1 - a_o2) * a_h1

∂E_t/∂w8 = (a_o2 - t2) * a_o2 * (1 - a_o2) * a_h2

*Part -4 The below steps shows how derivative of the error/loss is calculated with respect to the weights for the hidden layer*

Lets take the path from E_total to ah1

E1 -> a_o1 -> o1 -> a_h1
E2 -> a_o2 -> o2 -> a_h1

Hence, we have the below derivatives for a_h1

∂E1/∂a_h1 = ∂E1/∂a_o1 * ∂a_o1/∂o1 * ∂o1/∂a_h1 = (a_o1 - t1) * a_o1 * (1 - a_o1) * w5
∂E2/∂a_h1 = ∂E2/∂a_o2 * ∂a_o2/∂o2 * ∂o2/∂a_h1 = (a_o2 - t2) * a_o2 * (1 - a_o2) * w7
∂E_t/∂a_h1 = ∂E1/∂a_h1 + ∂E2/∂a_h1

Similarly for a_h2 we have

∂E1/∂a_h2 = ∂E1/∂a_o1 * ∂a_o1/∂o1 * ∂o1/∂a_h2 = (a_o1 - t1) * a_o1 * (1 - a_o1) * w6
∂E2/∂a_h2 = ∂E2/∂a_o2 * ∂a_o2/∂o2 * ∂o2/∂a_h2 = (a_o2 - t2) * a_o2 * (1 - a_o2) * w8
∂E_t/∂a_h2 = ∂E1/∂a_h2 + ∂E2/∂a_h2


Having reached at the above level we can now write the derivative equation for w1, w2, w3 and w4 as below - 

∂E_t/∂w1 = ∂E_t/∂a_h1 * ∂a_h1/∂h1 * ∂h1/∂w1 = ∂E_t/∂a_h1 * a_h1(1-a_h1) * i1

∂E_t/∂w2 = ∂E_t/∂a_h1 * ∂a_h1/∂h1 * ∂h1/∂w2 = ∂E_t/∂a_h1 * a_h1(1-a_h1) * i2

∂E_t/∂w3 = ∂E_t/∂a_h2 * ∂a_h2/∂h2 * ∂h2/∂w3 = ∂E_t/∂a_h2 * a_h2(1-a_h2) * i1

∂E_t/∂w4 = ∂E_t/∂a_h2 * ∂a_h2/∂h2 * ∂h2/∂w4 = ∂E_t/∂a_h2 * a_h2(1-a_h2) * i2



Based on the derivative values for weights, the weights were adjusted using the formula W_new = w_old - η*∂W_old where η is the learning rate the value used here is 0.5.

The below image shows how our excel performed - 


![](/Images/Excel_image1.png)

![](/Images/Excel_image1.png)
