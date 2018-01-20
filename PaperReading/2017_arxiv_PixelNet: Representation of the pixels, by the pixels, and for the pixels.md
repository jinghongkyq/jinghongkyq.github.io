### PixelNet: Representation of the pixels, by the pixels, and for the pixels.
2017 arxiv [Homepage](http://www.cs.cmu.edu/~aayushb/pixelNet/)

![1](https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/Pixelnet.png)

**Task**: general pixel-level prediction problems, from low-level edge detection to mid-level surface normal estimation to high-level semantic seg-
mentation.

**Motivation**: Convolutional predictors, such as the fully convolutional network (FCN), have achieved remarkable success by 
exploiting the spatial redundancy of neighboring pixels through convolutional processing. Though computationally efficient, 
we point out that such approaches are not statistically efficient during learning precisely because spatial redundancy limits 
the information learned from neighboring pixels.

**Contribution**: We demonstrate that stratified sampling of pixels allows one to 
> (1) add diversity during batch updates, speeding up learning; 
> (2) explore complex nonlinear predictors, improving accuracy;
> (3) efficiently train state-of-the-art models tabula rasa (i.e., “from scratch”) for diverse pixel-labeling tasks. 
