### PixelNet: Representation of the pixels, by the pixels, and for the pixels.
2017 arxiv [Homepage](http://www.cs.cmu.edu/~aayushb/pixelNet/)

![1](https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/Pixelnet.png)

**Task**: general pixel-level prediction problems, from low-level edge detection to mid-level surface normal estimation to high-level semantic seg-
mentation.

**Motivation**: 
>Convolutional predictors, such as the fully convolutional network (FCN), have achieved remarkable success by 
exploiting the spatial redundancy of neighboring pixels through convolutional processing. Though computationally efficient, 
we point out that such approaches are not statistically efficient during learning precisely because spatial redundancy limits 
the information learned from neighboring pixels.

>In this paper, we explore the tradeoff between statistical and computational efficiency for convolutional learning, and investigate simply sampling a modest number of pixels across a small number of images
for each SGD batch update, exploiting convolutional processing where possible.

**Contribution**: We demonstrate that stratified sampling of pixels allows one to 
1. add diversity during batch updates, speeding up learning; 
2. explore complex nonlinear predictors, improving accuracy;
3. efficiently train state-of-the-art models tabula rasa (i.e., “from scratch”) for diverse pixel-labeling tasks. 

In detail:

1. We experimentally validate that, thanks to spatial correlations between pixels, just sampling a small number of pixels per image is sufficient for learning. More importantly, sampling allows us to train end-to-end particular non-linear models not earlier possible, and explore several avenues for improving both the efficiency and performance of FCN-based architectures. 
2. In contrast to the vast majority of models that make use of pre-trained networks, we show that pixel-level optimization can be used to train models tabula rasa, or “from scratch” with simple random Gaussian initialization. Intuitively, pixel-level
labels provide a large amount of supervision compared to image-level labels, given proper accounting of correlations.
Without using any extra data, our model outperforms previous unsupervised/self-supervised approaches for semantic
segmentation on PASCAL VOC-2012 [26], and is competitive to fine-tuning from pre-trained models for surface normal estimation. 
3. Using a single architecture and without much modification in parameters, we show state-of-the-art performance for edge detection on BSDS [4], surface normal estimation on NYUDv2 depth dataset [83], and semantic segmentation on the PASCAL-Context dataset [68].

**Algorithm**:

hypercolumn features h_p(X) = [c_1(p), c_2(p),..., c_M(p)]
