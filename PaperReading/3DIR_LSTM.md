### [Facial Expression Recognition Using Enhanced Deep 3D Convolutional Neural Networks](http://openaccess.thecvf.com/content_cvpr_2017_workshops/w41/papers/Mahoor_Facial_Expression_Recognition_CVPR_2017_paper.pdf)
1. Model:3D ResNet + LSTM
![model](https://i.loli.net/2019/03/01/5c78e2bb16cf5.png)

2. Facial landmark enhancement:
* We incorporate the facial landmarks by replacing the shortcut in residual unit on original ResNet with element-wise multiplication of facial landmarks and the input tensor of the residual unit.
* Given the facial landmarks for each frame of a sequence, we initially resize all of the images in the sequence to their corresponding filter size in the network. 
* Afterwards, we assign weights to all of the pixels in a frame of a sequence based on their distances(Manhattan distance) to the detected landmarks.
![1](https://i.loli.net/2019/03/01/5c78e44725bd2.png)
![2](https://i.loli.net/2019/03/01/5c78e4672e79e.png)

3. Result
* Subject-independent task
![si](https://i.loli.net/2019/03/01/5c78e49dacbeb.png)
* Cross-database task
![cd](https://i.loli.net/2019/03/01/5c78e4d706e15.png)