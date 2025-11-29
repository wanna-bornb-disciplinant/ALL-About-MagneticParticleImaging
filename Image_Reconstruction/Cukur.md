| Paper Name | Year | Publication Venue | Author(1st & Corr.) | Short Summary | Item Number | 
|------|------|------|------|------|------|
| Comparison of System-Matrix-Based and Projection-Based Reconstructions for Field Free Line Magnetic Particle Imaging | 2017 | International Journal on Magnetic Particle Imaging | Serhat Ilbey，Tolga Çukur | 比较了基于FFL的投影成像和系统矩阵成像的性能，主要学习这篇文章对这两类方法的具体实现 | 2017.1 | 
| TranSMS: Transformers for Super-Resolution  Calibration in Magnetic Particle Imaging | 2022 | Alper Gungor，Tolga Cukur |  混合架构实现低分辨率系统矩阵的超分 | 2022.1 |

* **#2017.1**  
  **看文本的初衷是ADMM算法在系统矩阵中的用法，本文的主旨是对比了基于FFL的系统矩阵重建方法和投影重建的重建质量和重建时间，其中投影重建用到了投影X-Space+逆拉东变换；基于系统矩阵的重建对比了ADMM和nonnegative fused lasso(NFL)的效果**，其中NFL的方法在"M. Storath, C. Brandt, M. Hofmann, T. Knopp, J. Salamon, A. Weber, and A. Weinmann. Edge Preserving and Noise Reducing Reconstruction for Magnetic Particle Imaging. IEEE Trans. Med. Imag., 36(1):74–85, 2017."这篇文章中有详细说明。

  一些基础的实验设置：FFL梯度场强度为2T/m，成像大小为48mm*48mm，单个网格点大小为300um *300um，即160 *160的网格节点划分。FFL每次旋转的角度为3度，使用25nm直径的粒子，驱动场场强为60mT，采样频率为10MHz，成像时仅使用1.25MHz以下的频率分量，为消除磁场直馈去除掉了一直到一次谐波的以下全部频率分量，根据SSIM和不同SNR值(无噪音、30分贝、20分贝和10分贝)的标准化均方误差(nRMSE)将重建的图像与参考图像进行比较，其中相对于过滤前原始接收的时间域信号的规范来计算噪音功率。

  

  

