| Paper Name | Year | Publication Venue | Author(1st & Corr.) | Short Summary | Item Number | 
|------|------|------|------|------|------|
| Tomographic Field Free Line Magnetic Particle Imaging With an Open-Sided  Scanner Configuration | 2020 | TMI | Can Barıs Top, Alper Güngör | 效果很好的Open-Sided MPI扫描仪设计 | 2020.1 | 

* **#2020.1**  
  这篇文章是土耳其组在2020年发表的一篇关于open-sided MPI扫描仪搭建和设计的TMI，主要的卖点在于基于FFL的扫描仪设计第一次做到了真正的open-sided，即这个扫描仪中只在单个方向上布置了线圈就可以在理论上实现三维的MPI重建，在重建方法上采用L1+TV的正则化，通过ADMM交替优化最后的系统矩阵线性方程组，同时对系统矩阵做了一个类似上采样的插值处理，相应的也对方程做了一个改写，整个重建过程是土耳其组的老套路，也仍然在系统矩阵的获取阶段使用了白化等手段，自己设计了两组总计三个Phantom，空间分辨率为2.5mm，采样灵敏度为11ug/mL，根据上下线圈的距离可以动态调整梯度场大小，采样FOV大小为34mm * 18mm，因为总计60个变化角度和单个角度下采集126个频率分量，总的系统矩阵大小为 15120 * 153
