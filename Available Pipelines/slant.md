# Slant
---
## Table of Contents
1. [General Information](https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/slant.md#general-information)
2. [Examples](https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/slant.md#examples)
3. [Links](https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/slant.md#links)
---

### General Information
- Current Version: slant_gpu_v1.1.0
- Processor Name: slant_gpu_v1.1.0_processor.yaml
- Singularity Recipe and Code: [https://github.com/MASILab/SLANTbrainSeg](https://github.com/MASILab/SLANTbrainSeg)
- SHA256 Hash: slant_gpu_v1.1.0.simg (SHA256 dfbe54020e25e0b6b872263a637540790ceb16702584de77fa94bda679263c9e)

### Examples
<img src="https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/images/slant_ABCD_T1W3D.png" width="425" height="550">

### Links
- [GitHub Repo for Current Spider](https://github.com/MASILab/SLANTbrainSeg)
---
- [3D Whole Brain Segmentation using Spatially Localized Atlas Network Tiles](https://arxiv.org/pdf/1903.12152.pdf)

**Abstract**

Detailed whole brain segmentation is an essential quantitative technique in medical image analysis, which provides a non-invasive way of measuring brain regions from a clinical acquired structural magnetic resonance imaging (MRI). Recently, deep convolution neural network (CNN) has been applied to whole brain segmentation. However, restricted by current GPU memory, 2D based methods, downsampling based 3D CNN methods, and patch-based high-resolution 3D CNN methods have been the defacto standard solutions. 3D patch-based high resolution methods typically yield superior performance among CNN approaches on detailed whole brain segmentation (>100 labels), however, whose performance are still commonly inferior compared with state-ofthe-art multi-atlas segmentation methods (MAS) due to the following challenges: (1) a single network is typically used to learn both spatial and contextual information for the patches, (2) limited manually traced whole brain volumes are available (typically less than 50) for training a network. In this work, we propose the spatially localized atlas network tiles (SLANT) method to distribute multiple independent 3D fully convolutional networks (FCN) for high-resolution whole brain segmentation. To address the first challenge, multiple spatially distributed networks were used in the SLANT method, in which each network learned contextual information for a fixed spatial location. To address the second challenge, auxiliary labels on 5111 initially unlabeled scans were created by multi-atlas segmentation for training. Since the method integrated multiple traditional medical image processing methods with deep learning, we developed a containerized pipeline to deploy the end-to-end solution. From the results, the proposed method achieved superior performance compared with multi-atlas segmentation methods, while reducing the computational time from >30 hours to 15 minutes. The method has been made available in ([https://github.com/MASILab/SLANTbrainSeg](https://github.com/MASILab/SLANTbrainSeg)).

*Yuankai Huo, Zhoubing Xu, Yunxi Xiong, Katherine Aboud, Parasanna Parvathaneni, Shunxing Bao, Camilo Bermudez, Susan M. Resnick, Laurie E. Cutting, and Bennett A. Landman. “3D whole brain segmentation using spatially localized atlas network tiles” NeuroImage 2019.*

---
- [Spatially Localized Atlas Network Tiles Enables 3D Whole Brain Segmentation from Limited Data](https://arxiv.org/pdf/1806.00546.pdf)

**Abstract**

Whole brain segmentation on a structural magnetic resonance imaging (MRI) is essential in non-invasive investigation for neuroanatomy. Historically, multi-atlas segmentation (MAS) has been regarded as the de facto standard method for whole brain segmentation. Recently, deep neural network approaches have been applied to whole brain segmentation by learning random patches or 2D slices. Yet, few previous efforts have been made on detailed whole brain segmentation using 3D networks due to the following challenges: (1) fitting entire whole brain volume into 3D networks is restricted by the current GPU memory, and (2) the large number of targeting labels (e.g., > 100 labels) with limited number of training 3D volumes (e.g., 30 hours using MAS to ≈ 15 minutes using the proposed method. The source code is available online.

*Yuankai Huo, Zhoubing Xu, Katherine Aboud, Parasanna Parvathaneni, Shunxing Bao, Camilo Bermudez, Susan M. Resnick, Laurie E. Cutting, and Bennett A. Landman. “Spatially Localized Atlas Network Tiles Enables 3D Whole Brain Segmentation” In International Conference on Medical Image Computing and Computer-Assisted Intervention, MICCAI 2018.*
