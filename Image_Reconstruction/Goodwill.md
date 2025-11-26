| Paper Name | Year | Publication Venue | Author(1st & Corr.) | Short Summary | Item Number | 
|------|------|------|------|------|------|
| The X-space formulation of the magnetic particle imaging process: 1-D signal, resolution, bandwidth, SNR, SAR, and magnetostimulation | 2010 | TMI | Patrick W. Goodwill，Steven M. Conolly | 一维X-Space | 2010.1 | 
| Multidimensional x-space magnetic particle imaging | 2011 | TMI | Patrick W. Goodwill，Steven M. Conolly | 多维X-Space | 2011.1 | 
| The Impact of Filtering Direct-Feedthrough on the x-Space Theory of  Magnetic Particle Imaging | 2011 | SPIE Medical Imaging | Kuan Lu, Steven Conolly | 通过直流信号弥补基频信号丢失 | 2011.2 |
| Relaxation in X-Space Magnetic Particle Imaging | 2012 | TMI | Laura R. Croft, Steven M. Conolly | X-Space方法中对弛豫加以分析，一阶Debye理论 | 2012.1 | 

* **#2010.1**  
  **1D的文章不仅详细叙述了1D X-Space成像理论，还分析了X-Space理论下的分辨率、带宽、SNR、SAR等成像特性**。
  
  空间分辨率根据卷积核的FWHM确定，因此空间分辨率表示为梯度和粒子浓度的函数，尤其是粒子直径以三次方的形式与空间分辨率呈反比。
  
  影响MPI成像FOV大小的主要因素是磁刺激。
  
  带宽的分析稍微复杂(详见文章)，卷积公式中的卷积核是朗之万函数的导数，为了在DFT中方便表示，将朗之万函数表示为近似的洛伦兹函数(傅里叶变换的结果是离散的指数函数)，简化推导将粒子浓度表示为三维上的delta函数，消除掉卷积的积分形式，指定-3dB的带宽要求，其实就是在边界频率上的功率值为峰值功率的一半，计算得到：MPI扫描仪的带宽要求和朗之万函数中的k、梯度值、扫描速率成正比，这里引入了扫描速率，扫描速率用于表示FFP位置与时间的关系(文章这里的意思是无论FFP轨迹怎么变，当前时刻都能得到一个线性变化参数)。
  
  进一步分析容易得到的结论是，空间分辨率和带宽之间有一个tradeoff，两者是正相关的成像特性，但之前分析的接收端的线圈带宽有限，再给定带宽的情况下，最终接收到的信号通过了一个brick-wall filter，相当于扩大了X-Space方法的卷积核FWHM，造成分辨率的进一步丢失。
  
  SNR的分析同样建立在带宽的分析基础上，可以得到粒子分布下的最大信号值(即卷积核峰值处)，通过建模放大器噪声、接收线圈噪声和体噪声，将噪声设置为玻尔兹曼噪声，通过SNR的计算公式计算，并引入了对3D情况下X-Space的分析(这里就是典型的一维笛卡尔轨迹)，得到三维的SNR与粒子直径、信道数、磁粒子中心磁化强度、FOV大小和梯度场强度等因素有关。

  **实验在zerodimensional MPI spectrometer进行**，通过一个静态均匀磁场模拟一个放置样本的位置，同时用另一个动态均匀磁场模拟FFP的运动情况，其实就是MPS的采集模式。

  文章涉及的1D X-Space推导如下：

  ![../pics/19.png](../pics/19.png)

* **#2011.1**
  **多维MPI中详细推导了多维MPI的信号方程和图像方程，介绍了X-Space方法实际解决MPI重建问题的流程，并对公式中的PSF包络做了详细的分析**。

  文章涉及的多维X-Space推导如下：
  
  ![../pics/20.png](../pics/20.png)
  ![../pics/21.png](../pics/21.png)
  ![../pics/22.png](../pics/22.png)

  上述第三张推导中提到了
  $ENV_T$和
  $ENV_N$这两个径向对称的标量(在朗之万函数或朗之万导数的部分的内容都是标量值)，这里文章一般采用切向和法向描述这两个PSF标量，划分标准是公式推导中按照切向和法向对总的向量导数做了分解，法向PSF标量通过数值分析的FWHM更宽(大概是切向的2.3倍，梯度设置是二维的-1和1的公倍数，这样的梯度场设置就使得PSF的空间形状是轴对称的)，切向PSF标量其实也就是一维X-Space方法中的PSF，因此法向PSF的出现使得多维X-Space的空间分辨率进一步下降。

  第二部分的分析是针对整个PSF的h(x)而言，假定此时的FFP方向是x轴的方向(这符合X-Space的使用场景，实际上在丽萨荣轨迹当中使用很少，更多的还是单线扫描平行移动的方法)，由于真实的卷积核是PSF乘上FFP速度，因此可以在三维情况下对PSF(h(x))进行拆分，大致的情况如下：

  ![../pics/23.png](../pics/23.png)

  共线的卷积核部分类似之前PSF的切向和法向的叠加，因此整体在二维的磁场设置下还是一个径向的包络形状，但垂直的卷积核部分不同，呈现出两个波峰的形状，这样叠加反而使得卷积核的形状大变，这也解释了与FFP速度贡献的PSF分量FWHM更小，代表着这个方向上更好的分辨率。

  多维X-Space方法真正用于重建还需要从信号方程中构建得到图像方程，其实就是将卷积以外的所有部分的影响全部消去，因为在多个方向中都会产生电压信号，因此MPI的图像方程处理方式是对每个时间点的电压信号点乘上该时刻的FFP速度(也可以看成是与FFP速度共线的方向上分辨率更高，所以才如此设置)，这样整体的公式如下：

  ![../pics/24.png](../pics/24.png)

  **重建中有两个问题需要解决，一个是插值，其实就是将某个时间点的电压信号对应到具体的空间位置，然后在划分的网格中对应到具体的某个像素点；另一个是解决基频信号丢失的问题，这个点在另一篇通过直流信号+Partial FOV的方式解决。X-Space方法其实并不关心如何解决反卷积问题，作为一种无需重建公式、实时对应到具体位置的浓度信息的重建方法，卷积核的blur效果本身就不是X-Space方法想考虑的部分**。

  这篇文章的实验部分是在真实的3D MPI设备中进行的，这台设备是典型的bore型闭合线圈拓扑，在bore的共线方向施加了驱动场，接收线圈也布置在孔径方向，因为FFP速度方向也是孔径方向不会发生改变。

* **#2011.2**  
  **本文解释了为什么通过直流信号弥补基频信号丢失并做了验证实验，另外补充了一些多维X-Space的实验细节**。

  首先一个出发点是基频信号丢失问题是普遍现象，并不是只有X-Space方法需要解决的问题，基于系统矩阵的方法同样需要针对性解决这个难点。

  
  
  
  

  
