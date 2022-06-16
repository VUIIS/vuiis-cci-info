# cat12_ss2p0

---
## Table of Contents
1. [General Information](https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/cat12_ss2p0.md#general-information)
2. [Examples](https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/cat12_ss2p0.md#examples)
3. [Links](https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/cat12_ss2p0.md#links)
---

### General Information

The cat12 spider runs the default preprocessing pipeline from the Computational Anatomy Toolbox for SPM. It is run on native space T1 images and provides outputs usable for Voxel Based Morphometry (VBM) analyses, Surface Based Morphometry (SBM; gyrification, sulcal depth and cortical thickness) and normalization from native space to MNI space (forward and inverse deformation fields).

**Important**

- Inputs
  - Native space T1 nifti
  - Set skull stripping parameters (0 – SPM approach; 0.5 – gcut; 2 – SPM+ approach; 3 – SPM+ approach & gcut)

**Version Information**

Current Version: cat12_ss2p0_v2.0.0
Processor Name: cat12_ss2p0_v2.0.0.yaml
SHA256 Hash: cat12_singularity_v2.simg (SHA256 a628f174a18367b1eaad8050a9ff8ac3ae762d4a028e9c8404c51a974c721006)

### Examples

**VUIIS_ABCD**

- T<sub>1</sub>-Weighted PDF: [cat12_ss2p0_v2](https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/pdfs/cat12_ss2p0_v2.pdf)

<img src="https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/images/cat12_T1W_ABCD.png" width="425" height="550">

**LANDMAN_UPGRAD**

- T<sub>1</sub>-Weighted PDF: [cat12_ss2p0_v2](https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/pdfs/catreport_t1_T1W.pdf)

<img src="https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/images/cat12_T1W_LU.png" width="425" height="550">

- T<sub>1</sub> PDF: [cat12_ss2p0_v2](https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/pdfs/catreport_t1_T1.pdf)

<img src="https://github.com/VUIIS/vuiis-cci-info/blob/main/Available%20Pipelines/images/cat12_T1_LU.png" width="425" height="550">

### Links

– [GitHub Repo for Current Spider](https://github.com/annashuangvumc/cat12_ndw)

---

– [Website](https://www.neuro.uni-jena.de/cat/)

---

– [Unified segmentation](https://www.sciencedirect.com/science/article/abs/pii/S1053811905001102?via%3Dihub)

**Abstract**

A probabilistic framework is presented that enables image registration, tissue classification, and bias correction to be combined within the same generative model. A derivation of a log-likelihood objective function for the unified model is provided. The model is based on a mixture of Gaussians and is extended to incorporate a smooth intensity variation and nonlinear registration with tissue probability maps. A strategy for optimising the model parameters is described, along with the requisite partial derivatives of the objective function.

*Ashburner J, Friston KJ. Unified segmentation. Neuroimage. 2005;26(3):839-851. doi:10.1016/j.neuroimage.2005.02.018*

---

– [A fast diffeomorphic image registration algorithm](https://www.sciencedirect.com/science/article/abs/pii/S1053811907005848?via%3Dihub)

**Abstract**

This paper describes DARTEL, which is an algorithm for diffeomorphic image registration. It is implemented for both 2D and 3D image registration and has been formulated to include an option for estimating inverse consistent deformations. Nonlinear registration is considered as a local optimisation problem, which is solved using a Levenberg–Marquardt strategy. The necessary matrix solutions are obtained in reasonable time using a multigrid method. A constant Eulerian velocity framework is used, which allows a rapid scaling and squaring method to be used in the computations. DARTEL has been applied to intersubject registration of 471 whole brain images, and the resulting deformations were evaluated in terms of how well they encode the shape information necessary to separate male and female subjects and to predict the ages of the subjects.

*Ashburner J. A fast diffeomorphic image registration algorithm. Neuroimage. 2007;38(1):95-113. doi:10.1016/j.neuroimage.2007.07.007*

---

– [Cortical thickness and central surface estimation](https://www.sciencedirect.com/science/article/abs/pii/S1053811912009603)

**Abstract**

Several properties of the human brain cortex, e.g., cortical thickness and gyrification, have been found to correlate with the progress of neuropsychiatric disorders. The relationship between brain structure and function harbors a broad range of potential uses, particularly in clinical contexts, provided that robust methods for the extraction of suitable representations of the brain cortex from neuroimaging data are available. One such representation is the computationally defined central surface (CS) of the brain cortex. Previous approaches to semi-automated reconstruction of this surface relied on image segmentation procedures that required manual interaction, thereby rendering them error-prone and complicating the analysis of brains that were not from healthy human adults. Validation of these approaches and thickness measures is often done only for simple artificial phantoms that cover just a few standard cases. Here, we present a new fully automated method that allows for measurement of cortical thickness and reconstructions of the CS in one step. It uses a tissue segmentation to estimate the WM distance, then projects the local maxima (which is equal to the cortical thickness) to other GM voxels by using a neighbor relationship described by the WM distance. This projection-based thickness (PBT) allows the handling of partial volume information, sulcal blurring, and sulcal asymmetries without explicit sulcus reconstruction via skeleton or thinning methods. Furthermore, we introduce a validation framework using spherical and brain phantoms that confirms accurate CS construction and cortical thickness measurement under a wide set of parameters for several thickness levels. The results indicate that both the quality and computational cost of our method are comparable, and may be superior in certain respects, to existing approaches.

*Dahnke R, Yotter RA, Gaser C. Cortical thickness and central surface estimation. Neuroimage. 2013;65:336-348. doi:10.1016/j.neuroimage.2012.09.050*

---

– [Topological Correction of Brain Surface Meshes Using Spherical Harmonics](https://link.springer.com/chapter/10.1007/978-3-642-04271-3_16)

**Abstract**

A brain surface reconstruction allows advanced analysis of structural and functional brain data that is not possible using volumetric data alone. However, the generation of a brain surface mesh from MRI data often introduces topological defects and artifacts that must be corrected. We show that it is possible to accurately correct these errors using spherical harmonics. Our results clearly demonstrate that brain surface meshes reconstructed using spherical harmonics are free from topological defects and large artifacts that were present in the uncorrected brain surface. Visual inspection reveals that the corrected surfaces are of very high quality. The spherical harmonic surfaces are also quantitatively validated by comparing the surfaces to an “ideal” brain based on a manually corrected average of twelve scans of the same subject. In conclusion, the spherical harmonics approach is a direct, computationally fast method to correct topological errors.

*Yotter R.A., Dahnke R., Gaser C. (2009) Topological Correction of Brain Surface Meshes Using Spherical Harmonics. In: Yang GZ., Hawkes D., Rueckert D., Noble A., Taylor C. (eds) Medical Image Computing and Computer-Assisted Intervention – MICCAI 2009. MICCAI 2009. Lecture Notes in Computer Science, vol 5762. Springer, Berlin, Heidelberg*

---

– [Algorithms to Improve the Reparameterization of Spherical Mappings of Brain Surface Meshes](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1552-6569.2010.00484.x)

**Abstract**

A spherical map of a cortical surface is often used for improved brain registration, for advanced morphometric analysis (eg, of brain shape), and for surface‐based analysis of functional signals recorded from the cortex. Furthermore, for intersubject analysis, it is usually necessary to reparameterize the surface mesh into a common coordinate system. An isometric map conserves all angle and area information in the original cortical mesh; however, in practice, spherical maps contain some distortion. Here, we propose fast new algorithms to reduce the distortion of initial spherical mappings generated using one of three common spherical mapping methods. The algorithms iteratively solve a nonlinear optimization problem to reduce distortion. Our results demonstrate that our correction process is computationally inexpensive and the resulting spherical maps have improved distortion metrics. We show that our corrected spherical maps improve reparameterization of the cortical surface mesh, such that the distance error measures between the original and reparameterized surface are significantly decreased.

*R. A. Yotter, P. M. Thompson, and C. Gaser, “Algorithms to improve the reparameterization of spherical mappings of brain surface meshes,” Journal of Neuroimaging, vol. 21, no. 2, pp. e134–e147, 2011.*
