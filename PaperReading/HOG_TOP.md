### [Facial Expression Recognition in Video with Multiple Feature Fusion](https://ieeexplore.ieee.org/document/7518582)

* Two main streams of facial expressions analysis are widely adopted in the current research and development:
  1. Detecting facial actions(FACS)
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

* **Geometric warp feature**
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

* [Acoustic Feature](https://sail.usc.edu/publications/files/schuller2010_interspeech.pdf)
  * The 38 low-level descriptors shown in Table 1 are first extracted and smoothed by simple moving average low-pass filtering.
  * After that, 21 functionals are employed and 16 zero-information features are eliminated.
  * Finally, two single features: the number of onsets (F0) and turn duration are added.


#### Feature fusion(Multi kernel SVM)
* SVM
  * Primal optimization problem
  ![primal](https://i.loli.net/2018/11/18/5bf10e3b418fe.png)
  * Dual problem
  ![dual](https://i.loli.net/2018/11/18/5bf10e57c9ec1.png)
* Multi kernels
![multi](https://i.loli.net/2018/11/18/5bf10e8d230a8.png)
![multi](https://i.loli.net/2018/11/18/5bf10ecc13b24.png)
* Optimization
  * We set two nested iterative loops to optimize both the classifier and kernel combination weights. In the **outer loop, we adopt the grid search to find the kernel weight $\beta$**. In the **inner iteration, a solver of SVM is implemented by fixing the kernel weight $\beta$ to find the coefficients $\alpha$**. 
  * **One-versus-one** method is employed to deal with the multiclass-SVM problem and **max-win voting strategy** is adapt to do the classification. 

#### Data set
1. Extended Cohn-Kanade data set (CK+)
2. GEMEP-FERA 2011 data set
3. Acted Facial Expression in Wild (AFEW) 4.0 data set

Back to [home](README.md)