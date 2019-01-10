### Deep Embedding Features for Salient Object Detection  
AAAI 2019  

**Motivation:**    
- downsampling operations such as pooling and convolution dramatically reduce the resolution of initial image, which degrade the details such as image boundary;
- simply integrating multi-level features often cause features cluttered, and thus cause the incorrect saliency detection results;

**Solution:**
- propose a novel approach that transforms prior information into an embedding space to select attentive features and filter out outliers for salient object detection.

**Algorithm:**  
- **ISP:** a backbone for Initial Saliency Prediction;  
- **FEN (Feature Embedding Network):** is trained to embed each pixel of the coarse map into a metric space, which incorporates much attentive features that highlight salient regions and suppress the response of non-salient regions;  
- **RFIN (Recursive Feature Integration Network):** Further, the embedded features are refined through a deep-to-shallow Recursive Feature Integration Network (RFIN) to improve the details of prediction maps;
- **GFRN (Guided Filter Refinement Network):** to alleviate the blurred boundaries, we propose a Guided Filter Refinement Network (GFRN) to jointly optimize the predicted results and the learnable guidance maps.

**Integrate multi-scale features with different methods:**  
![RFIN1](https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/RFIN1.png)

**Framework:**  
![RFIN_net](https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/RFIN_net.png)

**FEN (Feature Embedding Nework):**  
![FEN](https://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/PaperReading/data/RFIN2.png)








