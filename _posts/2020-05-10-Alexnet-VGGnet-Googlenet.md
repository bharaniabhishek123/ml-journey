## Full (simplified) **AlexNet** architecture:

[227x227x3] INPUT \
[55x55x96] CONV1: 96 11x11 filters at stride 4, pad 0 \
[27x27x96] MAX POOL1: 3x3 filters at stride 2 \
[27x27x96] NORM1: Normalization layer \
[27x27x256] CONV2: 256 5x5 filters at stride 1, pad 2 \
[13x13x256] MAX POOL2: 3x3 filters at stride 2 \
[13x13x256] NORM2: Normalization layer \
[13x13x384] CONV3: 384 3x3 filters at stride 1, pad 1 \
[13x13x384] CONV4: 384 3x3 filters at stride 1, pad 1 \
[13x13x256] CONV5: 256 3x3 filters at stride 1, pad 1 \
[6x6x256] MAX POOL3: 3x3 filters at stride 2 \
[4096] FC6: 4096 neurons \
[4096] FC7: 4096 neurons \
[1000] FC8: 1000 neurons (class scores)

## Details/Retrospectives 
First use of ReLU \
Layer norm \
Heavy Data Augmentation \
droput 0.5 \
batchsize 128 \
SGD Momentum 0.9 \
Learning rate 1e-2, reduced by 10 manually when validation acc. plateaus \
L2 weight decay 5e-4 \
7 CNN ensemble 18.2% -> 15.2% 

## VGGNet architecture 

Small filter size but deeper network. \
8 layers of AlexNet , 16-19 layers of VGGNet 

## Details/Retrospectives 
- only 3x3 conv. stride 1, pad 1 \
 - and 2x2 max pool stride 2.

Why use smaller filters ? \
The stack of 3 conv layer filters of 3x3 stride 1 will have same effective receptive field as 1 conv layer of 7x7. \
Although the network will become deeper and will have more non-linearities. \
But will have fewer parameters \
3 * (3^2 C^2) vs (7^2 C^2) \
- No layernorm 
- Uses ensemble for better results 

## GoogleNet 
- 22 layers 
- few parameters 5 million 
- Efficient "Inception Module" 
- No FC (affine) layers


## Calculating effective receptive field size over input.


Effective receptive field is calculated over the input, and iteratively as : \
n = k + s (m - 1) \
n = output \
k = filter size \
m = no. of pixel in current activation map that we want receptive field for \
s = stride 


![Here is computation](receptive_field.jpg)