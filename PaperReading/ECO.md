### [ECO: Efficient Convolutional Network for Online Video Understanding](http://openaccess.thecvf.com/content_ECCV_2018/papers/Mohammadreza_Zolfaghari_ECO_Efficient_Convolutional_ECCV_2018_paper.pdf)
---
#### why?
1. Firstly, a good initial classification of an action can already be obtain from just a single frame.
2. Secondly, to capture the contextual relationships between distant frames, a simple aggregation of scores is insufficient.

#### how?
1. Sample a fixed number of frames from the entire video to cover long-range temporal structure for understanding of video, the sampled frames span the entire video independent of the length of the video.
2. Use a 3D-network to learn the relationship between the frames and track them  throughout the video.
3. The network directly provides video-level scores without post-hoc feature aggregation.

#### Two architectures
* **ECO-lite**
![lite](https://i.loli.net/2018/11/15/5bed035a75562.png)

* **ECO-full**
![full](https://i.loli.net/2018/11/15/5bed051156240.png)

* **Network detail**
![detail](https://i.loli.net/2018/11/15/5bed0c548b05c.png)

#### Result
1. 
![result1](https://i.loli.net/2018/11/15/5bed0abec0b9f.png)
2. 
![result2](https://i.loli.net/2018/11/15/5bed0ae5505d0.png)
3. 
![result3](https://i.loli.net/2018/11/15/5bed0ba01920b.png)
4. 
![result4](https://i.loli.net/2018/11/15/5bed0bd995dad.png)
5. 
![result5](https://i.loli.net/2018/11/15/5bed0bfa4cd3a.png)


Back to [home](README.md)