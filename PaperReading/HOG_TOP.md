### [Facial Expression Recognition in Video with Multiple Feature Fusion](https://ieeexplore.ieee.org/document/7518582)

* Two main streams of facial expressions analysis are widely adopted in the current research and development:
  1. Detecting facial actions
  2. Carry out facial affect(emotion) recognition derectly

* Two main kinds of methods:
  1. Appearance based methods(feature descriptor)
  2. Geometry based methods

#### Main idea
* **HOG-TOP**(Histogram of Oriented Gradients from Three Orthogonal Planes) to characterize facial appearance changes.
* **Geometric warp feature** to capture facial configuration changes.
* **Acoustic feature** to provide complementary information.
![main](https://i.loli.net/2018/11/16/5bee3277e555e.png)

#### Methods
* **HOG-TOP**
  * The XY plane provides spatial appearance, and XT and YT planes record temporal or motion information.
  ![top](https://i.loli.net/2018/11/17/5befbbf56eeed.png)
  * Features:
  ![feature](https://i.loli.net/2018/11/17/5befc64717920.png)
  * Block based method:
  ![block](https://i.loli.net/2018/11/17/5befc688c9bb5.png)

* **Geomertic warp feature**
  * Derived from the warp transform of the facial landmarks
  * Divide the face area into some triangles using the facial landmarks
  ![landmark](https://i.loli.net/2018/11/17/5befee74e8a83.png)
  * The transform is shown as:
  ![trans](https://i.loli.net/2018/11/17/5beff2be7091e.png)
  ![trans2](https://i.loli.net/2018/11/17/5beff2fde30ba.png)
  Eq.(5) is obtained from:
  ![eq23](https://i.loli.net/2018/11/17/5beff4834c69a.png)
  ![eq4](https://i.loli.net/2018/11/17/5beff45aaee09.png)
  * the coefficients $a_1$ ~ $a_6$ are gathered and **concatenated** to form the geometric feature