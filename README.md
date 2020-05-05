# Shape Network

This repository is tensorflow 1.14 implementation of Shape Network, which extends [Fully Convolutional Network](http://arxiv.org/pdf/1605.06211v1.pdf)

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Result](#result)

## Overview

The shape network is designed to add low level feature to FCN predictions. Basically, it uses skip net structure, which introduced by FCN.

It takes convolutional layers from VGGNet(with out pooling) and concat with result from skip structure in FCN. The architecture is shown below.

<div align="center">
  <img src="https://user-images.githubusercontent.com/13795717/81071032-14909800-8f1f-11ea-85c7-d73f6fd9f985.PNG" alt="shape network architecture" width="800">
</div>

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

Cross Entropy through training is shown as below.

<div align="center">
  <img src="https://user-images.githubusercontent.com/13795717/80185151-d35ad700-8646-11ea-8acb-94f36f7ed715.PNG" alt="cross_entropy_shape_network_256_to_64" width="200" height="150">

  <img src="https://user-images.githubusercontent.com/13795717/80185183-e1105c80-8646-11ea-85e6-20a17382e924.PNG" alt="cross_entropy_shape_network_256_to_128" width="200" height="150">

  <img src="https://user-images.githubusercontent.com/13795717/80185204-eff70f00-8646-11ea-8cf0-fd71e65d8d25.PNG" alt="cross_entropy_shape_network_256_to_256" width="200" height="150">
  
</div>

[Dice coefficient](https://en.wikipedia.org/wiki/S%C3%B8rensen%E2%80%93Dice_coefficient), sensitivity and specificity are used as metric of model's performance. 
The comparison of performance between Shape Network and FCN is shown as below.

<div align="center">
  <img src="https://user-images.githubusercontent.com/13795717/81071398-9c76a200-8f1f-11ea-8356-4f9201dc9bd8.png" alt="Dice Coefficient" width="350">
  <img src="https://user-images.githubusercontent.com/13795717/81071483-c0d27e80-8f1f-11ea-972b-8c1ab250c692.png" alt="dice-coefficient-tumor" width="350">
</div>

<div align="center">
  <img src="https://user-images.githubusercontent.com/13795717/81071645-f9725800-8f1f-11ea-9639-aea945ed2eb3.png" alt="sensitivity" width="350">
  <img src="https://user-images.githubusercontent.com/13795717/81071684-068f4700-8f20-11ea-87b0-ab47bb171c2b.png" alt="specificity" width="350">
</div>

The visualized results are shown as below. 

### Case 1: Brats18_TCIA01_203

<div align="center">
  <p>Ground truth, mri image and Fully Covolutional Network predictions </p>
  <img src="https://user-images.githubusercontent.com/13795717/80208504-53933380-866b-11ea-9749-7c1550c53f6a.png" alt="Ground Truth" width="200" height="200">
  <img src="https://user-images.githubusercontent.com/13795717/80208505-555cf700-866b-11ea-8901-af3f36b20825.png" alt="inp" width="200" height="200">
  <img src="https://user-images.githubusercontent.com/13795717/80208512-5726ba80-866b-11ea-98b8-2be960aaffa2.png" alt="FCN prediction" width="200" height="200">
</div>
<div align="center">
  <p>Shape network predictions</p>
  <img src="https://user-images.githubusercontent.com/13795717/80208653-a53bbe00-866b-11ea-921d-6dae8cb806db.png" alt="shapeNet ratio_256_to_64 prediction" width="200" height="200">
  <img src="https://user-images.githubusercontent.com/13795717/80208671-aec52600-866b-11ea-8fab-c7173e63e220.png" alt="shapeNet ratio_256_to_128 prediction" width="200" height="200">
  <img src="https://user-images.githubusercontent.com/13795717/80208721-c7354080-866b-11ea-9fcf-5bc809477354.png" alt="shapeNet ratio_256_to_256 prediction" width="200" height="200">
</div>

### Case 2: Brats18_TCIA06_409

<div align="center">
  <p>Ground truth, mri image and Fully Covolutional Network predictions </p>
  <img src="https://user-images.githubusercontent.com/13795717/80210768-48420700-866f-11ea-8d68-82a05993bc6d.png" alt="Ground Truth" width="200" height="200">
  <img src="https://user-images.githubusercontent.com/13795717/80210764-47a97080-866f-11ea-9f71-583e0cdc233d.png" alt="inp" width="200" height="200">
  <img src="https://user-images.githubusercontent.com/13795717/80210770-48da9d80-866f-11ea-85d0-4ccfee09bf2a.png" alt="FCN prediction" width="200" height="200">
</div>


<div align="center">
  <p>Shape network predictions</p>
  <img src="https://user-images.githubusercontent.com/13795717/80211067-e9c95880-866f-11ea-8ddd-99f08c699c34.png" alt="shapeNet ratio_256_to_64 prediction" width="200" height="200">
  <img src="https://user-images.githubusercontent.com/13795717/80211080-f3eb5700-866f-11ea-9a7e-246428fd6310.png" alt="shapeNet ratio_256_to_128 prediction" width="200" height="200">
  <img src="https://user-images.githubusercontent.com/13795717/80211311-7542e980-8670-11ea-9881-7588f698061a.png" alt="shapeNet ratio_256_to_256 prediction" width="200" height="200">
</div>

