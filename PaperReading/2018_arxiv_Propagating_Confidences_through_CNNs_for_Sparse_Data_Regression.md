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

4. quantitative comparions

<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/PC5.png" width="50%" height="50%">

*NConv-1-Scale(16ch)*: architecture consists of 6 normalized convolution layers with filter sizes of 11 × 11, 7 × 7, 5 ×
5, 3 × 3, 3 × 3 and 1 × 1 respectively with 16 channels each.  
*NConv-1-Scale(4ch)*: same architecture, 4 channels each, much smaller number of parameters.  
*Nconv-HMS*: multiscale as illustrated in Figure 2.  
*scale-fusion scheme*: *Nconv-HMS* upsample the coarse scales, concatenate it with the finer scale, and then use a **normalized convolution** to learned the proper fuseion;  *Nconv-SF-STD* use the standard fusion.

5. qualitative analysis

<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/PC6.png" width="50%" height="50%">

> the output confidences from our method provide indication about how reliable the output depth maps are. At locations where neither input points nor groundtruth information is available, e.g. behind the cyclists or below the billboard, the output confidence is very low. Further, the results show that regions in the center of the scene tend to have high confidence due to the high point cloud density in the input. This demonstrates that our method for confidence propagation enables the network to learn the prominence of different regions with respect to the groundtruth.

<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/PC7.png" width="50%" height="50%">

>  As discussed earlier, our single-scale architecture suffers from a limited receptive field and fails to predict values for regions above the horizon in some images. This leads to a significant increase in the RMSE. We addressed this problem by adopting a multiscale architecture to cover the whole receptive field.   

> For the case of the multi-scale architecture, the error is mainly distributed along sharp edges and upon the horizon. This is likely due to the absence of structural information that could be found in RGB images. As shown in Figure 4, errors are distributed along the vehicles edges and close to the horizon. This problem could be addressed by incorporating prior knowledge about the structure of the scene from the RGB image.









