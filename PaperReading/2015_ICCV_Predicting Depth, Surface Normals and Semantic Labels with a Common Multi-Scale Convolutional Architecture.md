### Predicting Depth, Surface Normals and Semantic Labels with a Common Multi-Scale Convolutional Architecture
2015 ICCV 
[Homepage](http://cs.nyu.edu/~deigen/dnl/)

**Goals**: using a single multiscale convolutional network architecture: depth prediction, surface normal estimation, and semantic labeling.

![1](https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/1.png) ![2](https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/2.png)

**Framework**
Our model is a multi-scale deep network that first predicts a coarse global output based on the entire image area,
then refines it using finer-scale local networks.
* Scale 1: Full-Image View
> The first scale in the network predicts a coarse but spatially-varying set of features for the entire image area, we accomplish this through the use of two fully-connected layers. The output of the last full layer is reshaped to 1/16-scale in its spatial dimensions by 64 fea tures, then upsampled by a factor of 4 to 1/4-scale.

* Scale 2: Predictions
> The job of the second scale is to produce predictions at a mid-level resolution.

> concatenating the feature maps of the coarse network with those from a single layer of convolution and pooling, performed at finer stride.

> The output of the second scale is a 55x74 prediction (for NYUDepth), with the number of channels depending on the task, train Scales 1 and 2 of the model jointly.

* Scale 3: Higher Resolution
> The final scale of our model refines the predictions to higher resolution.

> concatenate the Scale-2 outputs with feature maps generated from the original input at yet finer stride.

> The final output resolution is half the network input.
