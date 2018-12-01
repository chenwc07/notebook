### [Deep Facial Expression Recognition: A Survey](https://arxiv.org/pdf/1804.08348.pdf)

#### Datebase
![data](https://i.loli.net/2018/11/22/5bf64ddc0b792.png)

or [more](https://www.behance.net/gallery/10675283/Facial-Expression-Public-Databases)

#### Pre-processing
##### 1. Face alignment
![align](https://i.loli.net/2018/11/22/5bf65ce73ecfc.png)
In general, **cascaded regression** has become the most popular and state-ofthe-art methods for face alignment as its high speed and accuracy.

##### 2. Data augmentation
* On-the-fly data augmentation
* Offline data augmentation

##### 3. Face normalization
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
* **Automatically learn the key parts for facial expression[159][160]**

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
* Feature-level ensembles
* Decision-level ensembles

##### Multitask networks
* FER is intertwined with various factors, such as head pose, illumination, and subject identity (facial morphology)
* To solve this problem, multitask leaning is introduced to transfer knowledge from other relevant tasks and to disentangle nuisance factors

##### Cascaded networks
* Related studies have proposed combinations of different structures to learn a hierarchy of features through which factors of variation that are unrelated with expressions can be gradually filtered out.

##### Generative adversarial networks (GANs)
* GAN-based models for pose-invariant FER
* GAN-based models for identity-invariant FER

#### Deep FER networks for dynamic image sequences
##### Frame aggregation
Various methods have been proposed to aggregate the network output for frames in each sequence to improve the performance.
* Decision-level frame aggregation
* Feature-level frame aggregation

##### Expression Intensity network
Take training samples with different intensities as input to exploit the intrinsic correlations among expressions from a sequence that vary in intensity
* PPDN: peak-piloted deep network
* DCPN: deeper cascaded peak-piloted network
* More intensity states and five loss functions for different task

Considering that images with different expression intensities for an individual identity is not always available in the wild, several works proposed to automatically acquire the intensity label or to generate new images with targeted intensity.

##### Deep spatio-temporal FER network
Utilizing both textural and temporal information to encode more subtle expressions
**1. RNN and C3D:**
* RNN, LSTM, IRNN, BRNNS, Nested LSTM, T-LSTM, C-LSTM
* C3D has been widely used for dynamic-based FER
  * C3D
  * DPM-inspired deformable facial action
  * Deep temporal appearance network (DTAN)
  * Weighted C3D
  * C3D with DBN
  * C3D with NetVLAD

**2. Facial landmark trajectory:**
* The most direct way is to concatenate coordinates of facial landmark points from frames over time with normalization to generate a onedimensional trajectory signal for each sequence
* Form an image-like map as the input of CNN
* Relative distance variation of each landmark in consecutive frames can also be used to capture the temporal information
* Part-based model that divides facial landmarks into several parts according to facial physical structure and then separately feeds them into the networks hierarchically
* [[112]](http://openaccess.thecvf.com/content_cvpr_2017_workshops/w41/papers/Mahoor_Facial_Expression_Recognition_CVPR_2017_paper.pdf) incorporated the trajectory features by replacing the shortcut in the residual unit of the original 3D Inception-ResNet with element-wise multiplication of facial landmarks and the input tensor of the residual unit

**3. Cascaded networks:**
* Combining CNN with LSTM
* Sparse autoencoder and LSTM
* ResNet-LSTM
* Conditional random fields(CRFs)

**4. Network ensemble:**
* Multi-channel network that extractes the spatial information from emotion-expressing faces and temporal information(optical flow) from the changes between emotional and neutral faces
* PHRNN and MSCNN fusion
![fuse](https://i.loli.net/2018/12/01/5c0234632bab6.png)
* DTAN and DTGN joint training
![fuse2](https://i.loli.net/2018/12/01/5c023499f38c7.png)




