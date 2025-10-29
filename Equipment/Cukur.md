| Paper Name | Year | Publication Venue | Author(1st & Corr.) | Short Summary | Item Number | 
|------|------|------|------|------|------|
| Tomographic Field Free Line Magnetic Particle Imaging With an Open-Sided  Scanner Configuration | 2020 | TMI | Can Barıs Top, Alper Güngör | 效果很好的Open-Sided MPI扫描仪设计 | 2020.1 | 

* **#2020.1**  
  这篇TMI的主要贡献是土耳其组在2020年搭建了一个open-sided FFL MPI扫描仪，扫描灵敏度在 $11ug/ml-770ug/ml$，在较低的0.6T/m的梯度场强度的基础上可以做到2.5mm的空间分辨率，仪器的上下线圈组可调，以便根据成像对象尺寸调整磁场梯度，其主要的卖点在于**基于FFL的扫描仪设计第一次做到了真正的open-sided，即这个扫描仪中只在单个方向上布置了线圈就可以在理论上实现三维的MPI重建**。
  文章在引言部分提到了在2020年的时间节点，MPI的载体和phantom研究已经证明了**MPI在以下领域中具有潜在用途**：实时心脏成像、心血管干预的仪器可视化、导管转向、非对称流体动力学评估、狭窄量化、细胞跟踪、肿瘤成像、灌流成像、胃肠道出血成像、温度成像、引导和聚焦高温治疗、吸入气雾剂的定量跟踪、前哨淋巴结检测、脑血容量成像、粘性映射等等。
  Closed bore FFL MPI扫描仪在之前已有发展，主要的两个分支就是最早的多个线圈形成一个环，构成的FFL场可以旋转+平移，后续这个线圈拓扑又有一定的改进；另外一个就是Goodwill组设计的两端放置线圈，在y方向上形成FFL进行投影成像的分支，**closed bore的设计对于磁场调控有天然的优势，但对于一些介入式研究而言，显然更需要open-sided的设计**，因此文章的想法应孕而生，single-sided的设计也是基于这样的想法，但**single-sided的问题是随着和线圈距离的增大效果越来越差，因此只适合在一些表面成像任务中使用**。  
  Open-sided的能让FFL旋转的线圈拓扑设计如下：  
<img src="pics/1.png" alt="Open-sided configuration for the electronically rotating FFL" width="50%" height="50%">
  
  
  在重建方法上采用L1+TV的正则化，通过ADMM交替优化最后的系统矩阵线性方程组，同时对系统矩阵做了一个类似上采样的插值处理，相应的也对方程做了一个改写，整个重建过程是土耳其组的老套路，也仍然在系统矩阵的获取阶段使用了白化等手段，自己设计了两组总计三个Phantom，空间分辨率为2.5mm，采样灵敏度为11ug/mL，根据上下线圈的距离可以动态调整梯度场大小，采样FOV大小为34mm * 18mm，因为总计60个变化角度和单个角度下采集126个频率分量，总的系统矩阵大小为 15120 * 153(17*9的grid size,60*126*2的频率分量，傅里叶变换的频域结果分离实部和虚部)
