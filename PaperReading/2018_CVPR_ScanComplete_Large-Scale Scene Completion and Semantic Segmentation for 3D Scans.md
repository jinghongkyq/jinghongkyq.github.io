### ScanComplete: Large-Scale Scene Completion and Semantic Segmentation for 3D Scans
2018 CVPR
[paper](https://arxiv.org/abs/1712.10215)  
[code](https://github.com/angeladai/ScanComplete)  

<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/scancomplete1.png" width="100%" height="100%">

**Abstract**  
  
<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/scancomplete2.png" width="50%" height="50%">

**Goal**
> scene completion  
> semantic segmentation  

**Challenges and Solutions**
> When represented with volumetric grids, data size grows cubically as the size of the space increases, which severely limits resolution.  
> Indoor scenes are particularly challenging, as they are not only large but can also be irregularly shaped with varying spatial extents.  

> We leverage fully-convolutional neural networks that can be trained on smaller subvolumes but applied to arbitrarily-sized scene environments at test time. This ability allows efficient processing of 3D scans of very large indoor scenes: we show examples with bounds of up to 1480×1230×64 voxels (≈ 70×60×3m).  
> To obtain high-quality output, the model must use a sufficiently high resolution to predict fine-scale detail. However, it must also consider a sufficiently large context to recognize large structures and maintain global consistency. To reconcile these competing concerns, we propose a coarse-to-fine strategy in which the model predicts a multi-resolution hierarchy of outputs. The first hierarchy level predicts scene geometry and semantics at low resolution but large spatial context. Following levels use a smaller spatial context but higher resolution, and take the output of the previous hierarchy level as input in order to leverage global context.  

**Methods**  
ScanComplete method: input: a aprtial 3D scan, represented by a truncated signed distance field (TSDF) stored in a volumetric grid.  

output: a truncated, unsigned distance field (TDF).  
At train time, we provide the network with a target TDF, which is generated from a complete ground-truth mesh. The network is trained to output a TDF which is as similar as possible to this target complete TDF.

Our network first predicts the output at a low resolution in order to leverage more global information from the input. Subsequent hierarchy levels operate at a higher resolution and smaller context size. They condition on the previous level’s output in addition to the current-level incomplete TSDF. We use three hierarchy levels, with a large context of several meters (∼ 6m3) at the coarsest level, up to a fine-scale voxel resolution of ∼ 5cm3; see Fig. 1.

<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/scancomplete3.png" width="100%" height="100%">  

**Data Generation**
[SUNCG dataset](http://suncg.cs.princeton.edu/).  
train scenes: 5359, test scenes: 155

**ScanComplete Network Architecture**  
<img src="https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/scancomplete4.png" width="100%" height="100%">  

use voxel grid resolutions of [32 × 16 × 32], [32 × 32 × 32], and [32 × 64 × 32] for each level, resulting
in spatial extents of [6m × 3m × 6m], [3m 3 ], [1.5m × 3m × 1.5m], respectively. For testing, we test on entire scenes.

At each hierarchy level, the network takes the input partial scan as input (encoded as an TSDF in a volumetric grid) as well as the previous low-resolution TDF prediction (if not the base level) and any previous voxel group TDF predictions. Each of the input volumes is processed with a series of 3D convolutions with 1×1×1 convolution shortcuts. They are then all concatenated feature-wise and further processed with 3D convolutions with shortcuts. At the end, the network splits into two paths, one outputting the geometric completion, and the other outputting semantic segmentation, which are measured with an L1 loss and voxel-wise softmax cross entropy, respectively.

**Loss**  
deterministic l1-distance, which forces the network to focus on a single mode. This setup is ideal when partial scans contain enough context to allow for a single explanation of the missing geometry.   
As another option, we use a probabilistic model formulated as a classification problem, i.e., TDF values are discretized into bins and their probabilities are weighted based on the magnitude of the TDF value. This setup may be better suited for very sparse inputs, as the predictions can be multi-modal.
