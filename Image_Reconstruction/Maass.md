| Paper Name | Year | Publication Venue | Author(1st & Corr.) | Short Summary | Item Number | 
|------|------|------|------|------|------|
| Deep image prior for 3D magnetic particle  imaging: A quantitative comparison of  regularization techniques on Open MPI dataset | 2020 | IWMPI | Soren Dittmer，Peter Maass | 在openmpi数据集上对比了DIP和其他正则化技术 | 2020.1 | 

* **# 2020.1**  
  这篇文章是最早的使用DIP作为MPI重建正则化项的文章，本身没有什么好说的，但在实验中对比得非常详细。将DIP的结果和多种不同正则化组合和不同优化算法的方式进行了比较，着重说一些比较重要的结论。

  首先OpenMPI上的数据处理方式是标准的全流程，即2019年那篇SNR阈值筛选+滤波选择+矩阵白化+rSVD都用了，因此是一个集大成的重建工作。

  DIP的网络设计上有创新，不再加入skip connection，使用三维的结构代替二维的，同时因为浓度非负且上界不为1的原因，选择ReLU的激活函数而不是Sigmoid。

  文章当中提到了处理系统矩阵和测量数据的方法，可以回头详细查看。

  在计算评价指标PSNR和SSIM的时候，选择了在2197个平移情况下的最大值，原因是：phantom 实际位置在scanning时有机器人机械误差、ground truth phantom的voxel grid与reconstruction grid并非完全对齐等等原因，导致phantom的离散化坐标值不一定能完美符合网格的剖分情况，因此考虑到-3mm到3mm，以0.5mm为一段的情况下，可能出现13*13*13=2197个偏离情况的可能，因此需要计算出每一种平移情况的指标，然后选择最大的一种，这个结论不是文章原创，借用了"T. Kluth and B. Jin, “L1 data fitting for robust numerical reconstruction in magnetic particle imaging: quantitative evaluation on Open MPI dataset.”"这篇文章中的观点。

  文章中和DIP做对比的VAR，实际上就是L1的loss加上了三种不同的正则化项，同时使用ICLR2018的AMSGrad进行优化得到的结果，详细可以看下面的对比，其中DIP也使用了L1的数据保真项；Kaczmarz中则使用了L2的数据保真项+正则化项、L2的数据保真项+L1和L2的正则化项、L2的数据保真项+L1的正则化项、L2的数据保真项+L1的正则化项+截断SVD的结果，详细的参数配置可以参照原文，指标对比如下：

  ![../pics/103.png](../pics/103.png)

  基于DIP的方法在两个指标中都获得最好效果；VAR中L1的数据保真项都会比L2要好；基于Kaczmarz的方法中L1+L2的正则化的效果是最好的，另外这篇文章的结论和前面提到的借鉴的那篇文章有一定的联系。
  
  
