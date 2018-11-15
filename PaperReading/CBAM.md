### [CBAM: Convolutional Block Attention Module](http://openaccess.thecvf.com/content_ECCV_2018/papers/Sanghyun_Woo_Convolutional_Block_Attention_ECCV_2018_paper.pdf)
***
#### Different way to improve the network performance
* Increase the depth (ResNet)
* Increase the width (GoogleNet)
* Increase the cardinality (ResNeXt)
  **Cardinality(分支)**
  ![cardinality](https://i.loli.net/2018/11/15/5bed1f6c9b7d4.png)

* Another aspect: **Attention**
  * Attention tells where to focus and improve the representation of interests
  * To increase representation power by using attention mechanism: focusing on important  features and suppressing unnecessary ones

#### Main idea
* Since convolution operations extract informative features by **blending cross-channel and spatial information together**, we adopt our module to **emphasize meaningful features along those two principal dimensions: channel and spatial axes.**
* Overview
  ![CBAM](https://i.loli.net/2018/11/15/5bed2297f1062.png)

#### Convolutional Block Attention Module
* Overall attention process
 ![overall](https://i.loli.net/2018/11/15/5bed2eb5171ca.png)
 During multiplication, the attention values are **broadcasted (copied)** accordingly: channel attention values are broadcasted along the spatial dimension, and vice versa. 

* Channel attention module
 ![channel](https://i.loli.net/2018/11/15/5bed301cc662a.png)
 The channel attention is computed as: 
 ![operation](https://i.loli.net/2018/11/15/5bed3206ef4bc.png)

* Spatial attention module
 ![spatial](https://i.loli.net/2018/11/15/5bed32d6efdf5.png)
 The spatial attention is computed as:
 ![operation](https://i.loli.net/2018/11/15/5bed33d779075.png)

#### Integrated with ResNet
The cubes in the picture are the **feature maps** 
![integrate](https://i.loli.net/2018/11/15/5bed359ae2385.png)

#### Result
* Image Classification
![image](https://i.loli.net/2018/11/15/5bed36fd24f64.png)

* Visualization
![visual1](https://i.loli.net/2018/11/15/5bed3754b3d56.jpg)
![visual2](https://i.loli.net/2018/11/15/5bed3789c1762.jpg)

Back to [home](README.md)