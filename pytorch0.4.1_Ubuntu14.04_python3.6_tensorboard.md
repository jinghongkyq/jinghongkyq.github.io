### Pytorch 0.4.1 + Ubuntu 14.04 + python 3.6 + tensorboard install with anaconda

**create environment**  
```
conda create -n your_env_name python=3.6
```

**install pytorch**   
go to website [pytorch official](https://pytorch.org/get-started/locally/), select the version you want.  
```
conda install pytorch torchvision cuda80 -c pytorch
```

**install tensorflow**  
go to website [tensorflow official](https://www.tensorflow.org/install/?hl=zh-cn)  
```
pip install tensorflow  # CPU ONLY
pip install tensorflow-GPU # CUDA-enabled
```

**install tensorboard**  
```
pip install tensorboardX
```

```
from tensorboardX import SummaryWriter   
writer = SummaryWriter('runs') # runs is a floder
# writer = SummaryWriter(comment='meow') # you can add a comment as suffix 

# add scalar
writer.add_scalar('Train/scalar_name', value, iteration) # value can be tensor/variable/numpy/float/int

# add image
# the form need to be [C*H*W], if images are in a batch [N*C*H*W], add_image will show them in suitable size.
# use np.transpose if you need
writer.add_image('Train/img_name', image, iteration)

# add text
writer.add_text('Train/text_name', 'write your text', iteration)

# pr curve
writer.add_pr_curve(tag, labels, predictions, step)

# figures of pyplot
# the figure generated by matplotlib.pyplot
writer.add_figure('Train/fig_name', figure, iteration)
```

**show the result**  
```
tensorboard --logdir=[your dir of 'runs']
```

you can also add `alias tb='tensorboard --logdir'` in `~/.bash_profile`, then do  
```
tb [your dir of 'runs']
```

copy and paste the link to browser.





