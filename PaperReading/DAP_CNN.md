### [Deeply Learning Deformable Facial Action Parts Model for Dynamic Expression Analysis](http://www.jdl.ac.cn/doc/2011/201511618541847969_2014_accv_deeply_learning_deformable_facial_action_parts_model_for_dynamic_expression_analysis.pdf)

1. DPM(Deformable Part Model)
* 物体检测模型，通过检测物体的主体(主模型)和物体的部分(子模型)并利用物体的部分与主体的相对位置的先验知识来计算总模型的可靠性来检测物体
2. Model in this paper
![model](https://i.loli.net/2019/02/25/5c73945e9d58d.png)
* S2 to C3 layer: 这里采用了N*c*k个检测滤波器来对特征图进行检测，其中N是预先定好的人脸部分，即假设人脸有N个关键部分, c是需要分类的表情种类, k是每一类的每一个部分的滤波器个数。
* S4 to D5 layer: 这里体现了DPM局部检测的思想, 这里$d_l$是加权向量, 这里$v_l$是每个部分的anchor point
  ![1](https://i.loli.net/2019/02/25/5c7396c3ad199.png)
  ![2](https://i.loli.net/2019/02/25/5c739701095f5.png)
  ![3](https://i.loli.net/2019/02/25/5c7397764c570.png)
3. Parameters initialization
* 3D filters: apply K-means clustering to learn centroids from the former feature maps and take them as the convolution filters
* connection weights: linear regression
![lr](https://i.loli.net/2019/02/25/5c739a4f67c54.png)
4. Result
![ck](https://i.loli.net/2019/02/25/5c739ac02469f.png)
![mmi](https://i.loli.net/2019/02/25/5c739aeae39f9.png)
![fear](https://i.loli.net/2019/02/25/5c739afd63270.png)