### [A visual attention based ROI detection method for facial expression recognition](https://www.sciencedirect.com/science/article/pii/S0925231218303266)

1. Model
![model](https://i.loli.net/2019/02/26/5c753474101a9.png)
对于CNN最后输出的大小为W×H×C的feature map, 对每一个空间位置的C个值用两层MLP学习出一个权值, 组成大小为W×H的weight map, 然后用这个weight map去加权每一个通道的特征, 相当于加权的average pooling

2. Result
![result](https://i.loli.net/2019/02/26/5c75381223f71.png)