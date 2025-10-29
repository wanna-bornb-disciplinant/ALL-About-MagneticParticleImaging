| Paper Name | Year | Publication Venue | Author(1st & Corr.) | Short Summary | Item Number | 
|------|------|------|------|------|------|
| Tomographic Field Free Line Magnetic Particle Imaging With an Open-Sided  Scanner Configuration | 2020 | TMI | Can Barıs Top, Alper Güngör | 效果很好的Open-Sided MPI扫描仪设计 | 2020.1 | 

* **#2020.1**  
  这篇TMI的主要贡献是土耳其组在2020年搭建了一个open-sided FFL MPI扫描仪，扫描灵敏度在 $11ug/ml-770ug/ml$，在较低的0.6T/m的梯度场强度的基础上可以做到2.5mm的空间分辨率，仪器的上下线圈组可调，以便根据成像对象尺寸调整磁场梯度，其主要的卖点在于**基于FFL的扫描仪设计第一次做到了真正的open-sided，即这个扫描仪中只在单个方向上布置了线圈就可以在理论上实现三维的MPI重建**。  
  文章在引言部分提到了在2020年的时间节点，MPI的载体和phantom研究已经证明了**MPI在以下领域中具有潜在用途**：实时心脏成像、心血管干预的仪器可视化、导管转向、非对称流体动力学评估、狭窄量化、细胞跟踪、肿瘤成像、灌流成像、胃肠道出血成像、温度成像、引导和聚焦高温治疗、吸入气雾剂的定量跟踪、前哨淋巴结检测、脑血容量成像、粘性映射等等。  
  Closed bore FFL MPI扫描仪在之前已有发展，主要的两个分支就是最早的多个线圈形成一个环，构成的FFL场可以旋转+平移，后续这个线圈拓扑又有一定的改进；另外一个就是Goodwill组设计的两端放置线圈，在y方向上形成FFL进行投影成像的分支，**closed bore的设计对于磁场调控有天然的优势，但对于一些介入式研究而言，显然更需要open-sided的设计**，因此文章的想法应孕而生，single-sided的设计也是基于这样的想法，但**single-sided的问题是随着和线圈距离的增大效果越来越差，因此只适合在一些表面成像任务中使用**。    
  Open-sided的能让FFL旋转的线圈拓扑设计如下(无论是在Cx线圈中还是在Cy线圈中，产生的磁场强度方向都是z方向的)：    
  <div style="text-align: center;">
    <img src=/pics/1.png alt="Open-sided configuration for the electronically rotating FFL" width="50%" height="50%">
  </div>
  文章通过Cx和Cy两组线圈的叠加产生可以旋转和平移的FFL，通过分析旋转和平移的坐标公式，确定了在两组线圈中需要施加的电流激励强度，另外为了控制一个与二维平面原点的距离(想象ycosθ = xsinθ + d)，需要再额外施加一个此方向上的电流激励，这部分的推导相对简单，可以自行查看原文，控制距离的这个磁场就可以视作此设备的focus field，而在之上施加的drive field则可以在一定程度上在原来的距离基础上调整这个距离。既然需要在Cx和Cy两组线圈之外额外施加一个距离磁场(实际上就是focus field)和一个激励磁场(实际上就是drive field)，因此一个很自然的问题就是如何布置额外的线圈满足这个要求，专门设计了一个驱动/聚焦线圈，即高幅值低频率的聚焦场和低幅值高频率(26KHz)的驱动场同时由一组线圈实现，在实现梯度场的线圈和实现驱动/聚焦场线圈之间用了铜片隔开，并设计了一种过滤匹配电路来抑制交流放大器的谐波和补偿驱动线圈的电感，接收线圈不多赘述，详细如下图：  
  <div style="text-align: center;">
    <img src=/pics/2.png alt="驱动/聚焦线圈和接收线圈的设计细节" width="50%" height="50%">
  </div>
  成像范围为34mm*18mm，梯度场线圈的间距为70mm，数据采集从0到177度每3度采集一次，共计60组数据，一次测量是整体过程，因此去除的背景信号是0度前和177度后的平均值。  
  在重建方法上采用L1+TV的正则化(不适用于所有的医学场景中)，通过ADMM交替优化最后的系统矩阵线性方程组，同时对系统矩阵做了一个类似上采样的插值处理(这个操作貌似是原创，即类似将一个像素分成了四个像素，扩大了系统矩阵的一维)，相应的也对方程做了一个改写，整个重建过程是土耳其组的老套路，也仍然在系统矩阵的获取阶段使用了白化等手段，自己设计了两组总计三个Phantom，总的系统矩阵大小为 15120 * 153(17*9的grid size,60*126*2的频率分量，傅里叶变换的频域结果分离实部和虚部)，这里值得注意的是引出了几篇文章匹配了土耳其组一贯的图像重建处理方式："Comparison of system-matrix-based and projection-based reconstructions for field free line magnetic particle imaging" 这篇文章描述的是ADMM中对重建逆问题的改写方式(正则项优化问题+数据保真项的限制)；"Edge preserving and noise reducing reconstruction for magnetic particle imaging"描述的是为什么使用L1-norm+TV的正则化处理；"Enhanced reconstruction in magnetic particle imaging by whitening and randomized SVD approximation"描述的是正问题求解和系统矩阵处理中为什么要SVD分解(加快迭代算法)和为什么要做系统矩阵白化。
  不分析结果了，反正就是还可以。
