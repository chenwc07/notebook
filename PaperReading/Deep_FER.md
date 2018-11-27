### [Deep Facial Expression Recognition: A Survey](https://arxiv.org/pdf/1804.08348.pdf)

#### Datebase
![data](https://i.loli.net/2018/11/22/5bf64ddc0b792.png)

or [more](https://www.behance.net/gallery/10675283/Facial-Expression-Public-Databases)

#### Pre-processing
#####1. Face alignment
![align](https://i.loli.net/2018/11/22/5bf65ce73ecfc.png)
In general, **cascaded regression** has become the most popular and state-ofthe-art methods for face alignment as its high speed and accuracy.

#####2. Data augmentation
* On-the-fly data augmentation
* Offline data augmentation

#####3. Face normalization
* Illumination normalization
* Pose normalization (frontalization)

#### Deep networks for feature learning
##### CNN
![CNN](https://i.loli.net/2018/11/22/5bf67374e5b04.png)
To read:
  * faster R-CNN[105]
  * 3D related methods[108,109]

##### DBN
Restricted Boltzmann machines(看不懂)

##### DAE
略
##### RNN
略
##### GAN
略

#### Classification
* softmax
* SVM
* deep neural forests
* Gaussian kernels on Symmetric Positive Definite (SPD) manifold

#### Deep FER networks for static images
##### Pre-training and fine-tuning
Using facial recognition database or object recognition database(ImageNet) and so on to pre-train the network, plus muti-stage fine-tuning strategy[111].

##### Diverse network input
* Low-level representations encode features(SIFT,LBP)
* Part-based representations extract features according to the target task
* Automatically learn the key parts for facial expression[159][160]

##### Auxiliary blocks & layers
* HoloNet: CReLU, Residual structure
* Inception-Residual block
* Supervised Scoring Ensemble(SSE)
![sse](https://i.loli.net/2018/11/26/5bfbe0c8e8c9e.png)
* Feature selection network(FSN)
* Assistance loss: Island loss, locality-preserving loss(LP loss), exponential triplet-based loss, (N+M)-tuples cluster loss

##### Network ensemble
* Two key factors:
(1) sufficient diversity of the networks to ensure complementarity
(2) an appropriate ensemble method that can effectively aggregate the committee networks

##### Multitask networks
* FER is intertwined with various factors, such as head pose, illumination, and subject identity (facial morphology)
* To solve this problem, multitask leaning is introduced to transfer knowledge from other relevant tasks and to disentangle nuisance factors
