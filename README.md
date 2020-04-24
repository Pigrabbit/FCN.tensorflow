# Shape Network

This repository is tensorflow 1.14 implementation of Shape Network, which extends [Fully Convolutional Network](http://arxiv.org/pdf/1605.06211v1.pdf)

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Result](#result)

## Overview

The shape network is designed to add low level feature to FCN predictions. Basically, it uses skip net structure, which introduced by FCN.

It takes convolutional layers from VGGNet(with out pooling) and concat with result from skip structure in FCN. The architecture is shown below.

![shape network architecture](https://user-images.githubusercontent.com/13795717/79685574-b99b4780-8274-11ea-94f0-77217a16a5a3.png)


## Prerequisites

- The dataset is not provided. You can download it [here](https://www.med.upenn.edu/sbia/brats2018/data.html)
  - After download, unzip it and place it into `./data` directory. 
- To train **Shape Network** execute `python shape_256_to_xx.py`
  - `256_to_xx` means the weight between Skip Structure Output and Low level feature.
  - There are three `256_to_xx` models, which are 64, 128 and 256.
- To train **FCN** model simply execute `python FCN.py`
- To visualize results for a random batch of images use flag `--mode=visualize`
  - You can find visualize image in `./logs/[MODEL_NAME]/visualize_result`
- To compute dice coefficient value, use flag `--mode=evaluate`
- `debug` flag can be set during training to add information regarding activations, gradients, variables etc.
- In `visualize_set.json`, brain ID to be evaluated and z-index of that brain are specified.
  - Dice coefficient is evalated based on these images.

## Result

Cross Entropy through training is shown below.

<p align="center">
  <img src="https://user-images.githubusercontent.com/13795717/80185151-d35ad700-8646-11ea-8acb-94f36f7ed715.PNG" alt="cross_entropy_shape_network_256_to_64" width="200" height="150">

  <img src="https://user-images.githubusercontent.com/13795717/80185183-e1105c80-8646-11ea-85e6-20a17382e924.PNG" alt="cross_entropy_shape_network_256_to_128" width="200" height="150">

  <img src="https://user-images.githubusercontent.com/13795717/80185204-eff70f00-8646-11ea-8cf0-fd71e65d8d25.PNG" alt="cross_entropy_shape_network_256_to_256" width="200" height="150">
</p>

Considering ratio between result of skip structure and low level feature, with higher low level feature ratio, it was able to get more detailed prediction image. While, more likely to False Positive and Low Dice coefficient. On the other hand, with lower low level fearue ratio, it was able to get higher Dice coefficient.

The visualized results are shown below. 

<p align="center">
<img src="https://user-images.githubusercontent.com/13795717/79687019-5c58c380-827f-11ea-8047-31077cd0e149.PNG" alt="brain case 1 gt-inp-fcn-shapeNet compare" width="500">
<img src="https://user-images.githubusercontent.com/13795717/79687007-4d721100-827f-11ea-85bb-0afc60c5cc01.PNG" alt="brain case 1 gt-inp-fcn-shapeNet compare" width="500">
</p>
