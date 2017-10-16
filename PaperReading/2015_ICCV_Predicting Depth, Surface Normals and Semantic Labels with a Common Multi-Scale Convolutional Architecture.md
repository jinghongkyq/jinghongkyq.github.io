### Predicting Depth, Surface Normals and Semantic Labels with a Common Multi-Scale Convolutional Architecture
2015 ICCV 
[Homepage](http://cs.nyu.edu/~deigen/dnl/)

**Goals**: using a single multiscale convolutional network architecture: depth prediction, surface normal estimation, and semantic labeling.

![1](https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/1.png) ![2](https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/2.png)

**Framework**
Our model is a multi-scale deep network that first predicts a coarse global output based on the entire image area,
then refines it using finer-scale local networks.
* Scale1: Full-Image View
> The first scale in the network predicts a coarse but spatially-varying set of features for the entire image area, we accomplish this through the use of two fully-connected layers. The output of the last full layer is reshaped to 1/16-scale in its spatial dimensions by 64 fea tures, then upsampled by a factor of 4 to 1/4-scale.

