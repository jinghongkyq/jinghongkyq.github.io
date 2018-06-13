### Propagating Confidences through CNNs for Sparse Data Regression
2018 arxiv  
[Paper](https://arxiv.org/abs/1805.11913)

**Abstract**

<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/PC1.png" width="50%" height="50%">

**Goal**: KITTI Depth Completion

**Related work**: Sparsity Invariant CNNs

<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/PC2.png" width="50%" height="50%">

the input is the projected LiDAR point cloud (RGB image optional), the goal is to densify the sparse depth map, the output is a complete dense map together with pixel-wise output confidence.

**challenges**: 
> handle missing values while also differentiate them from the zerio-valued regions.   
> the confidences are also desirable since they provide information about reliability of the output values. 

**methods**:
> In this paper, we propose an algebraically-constrained convolution operator for deep networks with sparse input to achieve a proper processing of confidences. The sparse input is equipped with confidences and the network is required to produce a dense output. We derive novel methods for determining the confidence from the convolution operation and propagating it to consecutive layers. To maintain the confidences within a valid range, we impose non-negativity constraints on the network weights during training. Further, we also introduce an objective function that simultaneously minimizes the data error while maximizing the output confidence. Moreover, we demonstrate the significance of the proposed confidence measure by introducing a novel approach for performing scale-fusion based on confidences.

> **normalized convolution** 

> **propagating confidence**

> **loss function**: Huber loss  
  The Huber norm helps preventing exploding gradients in case of highly sparse data, which stabilizes the convergence of the network.  
  New loss: minimize the error norm between the output and the GT (data term), increase the confidence of the output data (confidence term).  
  <img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/PC3.png" width="50%" height="50%">
  
**Network Architecture**

<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/PC4.png" width="50%" height="50%">

> Inspired by [9], we propose a hierarchical multi-scale architecture that shares the same weights between different scales, which leads to a very compact network as shown in Figure 2. Downsampling is performed using max pooling on the confidences and similar to [13] we keep the indices of the pooled pixels, which are then used to select the same pixels from the feature maps, i.e., we keep the most confident feature map pixels. The downsampled confidences are divided by the Jacobian of the scaling to maintain absolute confidence levels. Scale fusion is performed by upsampling the coarser scale and concatenate it with the finer scale. We apply a normalized convolution operator on the concatenated feature map to allow the network to fuse different scales utilizing confidence information.

**Experiments**

1. dataset: [KITTI Depth Completion Dataset](http://www.cvlibs.net/datasets/kitti/eval_depth.php?benchmark=depth_completion)
   86000 tranining images, 7000 validation images, 1000 unannotated test images. Evaluate on the full validation sets.

2. impementation details: batch size is 8; train on the first 10000 out of 86000 depth maps/images in the training set; ADAM solver with default parameters, lr=0.01.

3. evaluation metrics: *Mean Absolute Error (MAE)* which is an unbiased error metric, *Root Mean Square Error (RMSE)* which penalizes large errors, *Mean Absolute Relative Error (MRE)* is a ratio between the error magnitude and the groundtruth value, and *Inliers Ratio (δi)* which is the percentage of pixels having relative error less than a specific threshold to the power of i. As in [1], we use a challenging threshold value of δ = 1.01.




