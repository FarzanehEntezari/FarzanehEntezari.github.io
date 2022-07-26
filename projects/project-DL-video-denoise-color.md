---
title: Deep Learning for video denoising and colorization
layout: page
---

## Intro

Learning-based computational photography techniques demonstrate a potential capability of enhancing the camera systems without requiring a significant upgrade of hardware. Recently, deep neural networks have shown their superior performance in the imaging computation [1]. They can enhance the degraded images captured in bad work conditions, either to apply color constancy, deblur, denoise, colorize or super-resolution techniques.

Lighting conditions, camera sensitivity settings, electronic circuits and etc. can all lead the output to vary from the expected result; brighter or darker pixels or spurious color, which we define as noise. Therefore, one of the most demanding image computations is to reduce image noise and combat
imperfections. Another image computation which is of interest for numerous researchers is image or video colorization which aims to build a color version of image, given a gray-scale version. Colorizing historical black and white images or old movies is one of the applications which has gained lots of
attention. 
The goal of this project is to recover a color sharp video from a distorted version using Deep Neural Networks. The distorted video is a Full-HD size noisy black and white view of a lake surrounded by a bunch of trees. The video is downloaded from [2] and downgraded in two steps.


<video width="600px" height="500px" controls muted="" preload="true" autoplay = "autoplay" loop = "loop">
    <source src="../assets/img/projects/project-DL-video-denoise-color/project-DL-video-denoise-color.mp4" type="video/mp4">
</video> 

### Denoise frames

To reduce noise from images, we use a feed-forward denoising convolutional neural network (DnCNNs). In contrary with previous discriminative denoising models which were limited to additive white Gaussian noise (AWGN) at a certain noise level, this model is able to handle Gaussian denoising with unknown noise level (i.e.,blind Gaussian denoising). The model is a residual network which rather than directly outputing clean image, tries to predict the
residual image and separate noise from a noisy image. In order to enhance the performance, batch normalization techniques are also used in the proposed model.


In addition, a normalization step and a scale and shift step, called batch-normalization, is added before the nonlinearity function in each layer. This empowers the network to overcome sensitivity of the model to initialization and slow training process. Furthermore, to reduce boundary artifacts while
keeping the output image size the same as the input one, they pad zeros before every convolution. 

The structure of the model can be found in the video.

### Colorize frames

Several convolutional neural networks have been proposed to predict a color version of a scene by observing its gray-scale version. Predicting color images is an uncertainty problem as some objects can take several different colors (i.e. an apple can have red, green or yellow color). Therefore, the goal
of colorization problem is not to recover the ground truth color, but rather to hallucinate a plausible color image that a human can believe.

Taking the multimodel nature of the problem into consideration, we predict a probability distribution of colors for each pixel. Defining multinomial cross entropy as the loss function, we reweight the loss of each pixel at train time to balance the loss based on rare colors for that pixel. The annealed-mean of the distribution will be then mapped to point estimate color values.

The structure of CNN which predicts distribution over quantized color value outputs from a grayscale input is shown in the video.

