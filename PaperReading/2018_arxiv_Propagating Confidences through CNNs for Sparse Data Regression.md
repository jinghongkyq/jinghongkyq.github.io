### Propagating Confidences through CNNs for Sparse Data Regression
2018 arxiv

**Abstract**

<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/PC1.png" width="50%" height="50%">

**Goal**: KITTI Depth Completion

**Related work**: Sparsity Invariant CNNs

**Notes**  
<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/PC2.png" width="50%" height="50%">

the input is the projected LiDAR point cloud (RGB image optional), the goal is to densify the sparse depth map, the output is a complete dense map together with pixel-wise output confidence.

challenges: 
> handle missing values while also differentiate them from the zerio-valued regions. 
> the confidences are also desirable since they provide information about reliability of the output values. 

methods:
> In this paper, we propose an algebraically-constrained convolution operator for deep networks with sparse input to achieve a proper processing of confidences. The sparse input is equipped with confidences and the network is required to produce a dense output. We derive novel methods for determining the confidence from the convolution operation and propagating it to consecutive layers. To maintain the confidences within a valid range, we impose non-negativity constraints on the network weights during training. Further, we also introduce an objective function that simultaneously minimizes the data error while maximizing the output confidence. Moreover, we demonstrate the significance of the proposed confidence measure by introducing a novel approach for performing scale-fusion based on confidences.


