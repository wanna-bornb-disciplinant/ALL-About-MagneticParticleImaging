| Paper Name | Year | Publication Venue | Author(1st & Corr.) | Short Summary | Item Number | 
|------|------|------|------|------|------|
| Model-Based Reconstruction for Magnetic Particle Imaging in 2D and 3D | 2016 | Inverse Problems | März Thomas, Weinmann Andreas | 建立了一种新的MPI多维重建范式，构建了一个core operator | 2016.1 |

* **#2016.1**  
  主要是一种对标X-Space方法的分析算法，作者认为前面的分析法有两个巨大的问题：重建算法无法与扫描轨迹高度解耦；在多维情况下没有和低维一样有效且简介的类似标准卷积的前向算子；因此作者分析了MPI正问题，提出了一个core operator，核心算子建立在'phase space'上，完全与扫描轨迹脱钩，多维情况下通过求核心算子的迹将矩阵核转换为标准卷积核，重建算法核心是在n维下单个体素至少扫描n次，建立满秩矩阵计算得到对应phase space的核心算子，再进行反卷积操作(实际上也是通过计算loss极值，建立线性公式通过共轭梯度求解)
