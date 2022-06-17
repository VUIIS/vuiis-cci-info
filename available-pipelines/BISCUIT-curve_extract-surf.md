# BISCUIT, curve_extract, and surf_*

BISCUIT: Brain Shape Computing Toolbox – An Automated Pipeline for Cortical Morphometry

Brain Shape Computing Toolbox (BISCUIT) is a consolidated toolbox for cortical shape morphometry including (1) sulcal curve delineation for geometric feature extraction/ROI definition, (2) surface registration for cortical shape correspondence, and (3) local gyrification index for cortical shape quantification. These tools take an input mesh file(s) to generate and capture meaningful shape characteristics. BISCUIT is a wrapper of CMorph – a collection of surface processing tools.

**Important**

The following spiders are now a part of BISCUIT but are no longer supported by themselves:
- surf_postproc
- surf_quant
- surf_quant_stat
- curve_extract

**Requirements**

- biscuit_fs
  - FS6 pipeline
- biscuit_mc
  - macruise_multiatlas pipeline

**Version Information**

- Current Version: biscuit_fs_v2.0.0 & biscuit_mc_v2.0.0
- Processor Name: biscuit_fs_v2.0.0_processor.yaml & biscuit_mc_v2.0.0_processor.yaml
- Repositories: [https://github.com/ilwoolyu?tab=repositories](https://github.com/ilwoolyu?tab=repositories)
- SHA256 Hash: biscuit_FC_v2.0.simg (SHA256 bf71ad116187a237a30cddc1ab85074545358d799a9c67e730acd6d84efb225e)

**Patch Notes**

1. Version: 2.0.0 (6/22/2019)
  - HSD: improved performance and numerical accuracy
  - LGI: improved memory efficiency in klaplace
  - LGI: fixed numerical instability under certain circumstances
  - BISCUIT: improved PDF layouts

## Examples

**VUIIS_ABCD**

- T<sub>1</sub>-Weighted PDF: [biscuit_fs_v2](pdfs/biscuit_fs_v2_ABCD.pdf)
- T<sub>1</sub>-Weighted PDF: [biscuit_mc_v2](pdfs/biscuit_mc_v2_ABCD.pdf)
- T<sub>1</sub>-Weighted PDF: [CurvExtractionspider](pdfs/CurvExtractionspider.pdf)
- T<sub>1</sub>-Weighted PDF: [SurfPostProcspider](pdfs/SurfPostProcspider.pdf)
- T<sub>1</sub>-Weighted PDF: [SurfPostProcFsSpider](pdfs/SurfPostProcFsSpider.pdf)
- T<sub>1</sub>-Weighted PDF: [SurfQuantSpider](pdfs/SurfQuantspider.pdf)
- T<sub>1</sub>-Weighted PDF: [SurfQuantStatSpider](pdfs/SurfQuantStatspider.pdf)

**LANDMAN_UPGRAD**

- T<sub>1</sub>-Weighted PDF: [biscuit_fs_v2](pdfs/biscuit_fs_v2_T1W_LU.pdf)
- T<sub>1</sub> PDF: [biscuit_fs_v2](pdfs/biscuit_fs_v2_T1_LU.pdf)


## Code

- [Cortical surface registration](https://github.com/ilwoolyu/HSD)

- [Cortical surface protocols (brainCOLOR)](https://mindboggle.info/braincolor/)

– [Cortical surface protocols (Mindboggle)](https://mindboggle.readthedocs.io/en/latest/labels.html)

- [Cortical sulcal/gyral curve extraction](https://github.com/ilwoolyu/CurveExtraction)

- [Local gyrification index](https://github.com/ilwoolyu/LocalGyrificationIndex)

– [Shape complexity index](https://github.com/NIRALUser/ShapeComplexityIndex)


## References

- [Lyu, I., Kang, H., Woodward, N., Styner, M., Landman, B., Hierarchical Spherical Deformation for Cortical Surface Registration, Medical Image Analysis, 57, 72-88, 2019](https://pubmed.ncbi.nlm.nih.gov/31280090/) We present hierarchical spherical deformation for a group-wise shape correspondence to address template selection bias and to minimize registration distortion. In this work, we aim at a continuous and smooth deformation field to guide accurate cortical surface registration. In conventional spherical registration methods, a global rigid alignment and local deformation are independently performed. Motivated by the composition of precession and intrinsic rotation, we simultaneously optimize global rigid rotation and non-rigid local deformation by utilizing spherical harmonics interpolation of local composite rotations in a single framework. To this end, we indirectly encode local displacements by such local composite rotations as functions of spherical locations. Furthermore, we introduce an additional regularization term to the spherical deformation, which maximizes its rigidity while reducing registration distortion. To improve surface registration performance, we employ the second order approximation of the energy function that enables fast convergence of the optimization. In the experiments, we validate our method on healthy normal subjects with manual cortical surface parcellation in registration accuracy and distortion. We show an improved shape correspondence with high accuracy in cortical surface parcellation and significantly low registration distortion in surface area and edge length. In addition to validation, we discuss parameter tuning, optimization, and implementation design with potential acceleration.

- [Parvathaneni P, Bao S, Nath V, et al. Cortical Surface Parcellation using Spherical Convolutional Neural Networks. Med Image Comput Comput Assist Interv. 2019;11766:501‐509. doi:10.1007/978-3-030-32248-9_56](https://pubmed.ncbi.nlm.nih.gov/31803864/) We present cortical surface parcellation using spherical deep convolutional neural networks. Traditional multi-atlas cortical surface parcellation requires inter-subject surface registration using geometric features with slow processing speed on a single subject (2-3 hours). Moreover, even optimal surface registration does not necessarily produce optimal cortical parcellation as parcel boundaries are not fully matched to the geometric features. In this context, a choice of training features is important for accurate cortical parcellation. To utilize the networks efficiently, we propose cortical parcellation-specific input data from an irregular and complicated structure of cortical surfaces. To this end, we align ground-truth cortical parcel boundaries and use their resulting deformation fields to generate new pairs of deformed geometric features and parcellation maps. To extend the capability of the networks, we then smoothly morph cortical geometric features and parcellation maps using the intermediate deformation fields. We validate our method on 427 adult brains for 49 labels. The experimental results show that our method outperforms traditional multi-atlas and naive spherical U-Net approaches, while achieving full cortical parcellation in less than a minute.

- [Lyu I, Kim SH, Woodward ND, Styner MA, Landman BA. TRACE: A Topological Graph Representation for Automatic Sulcal Curve Extraction. IEEE Trans Med Imaging. 2018;37(7):1653‐1663. doi:10.1109/TMI.2017.2787589](https://pubmed.ncbi.nlm.nih.gov/29969416/) A proper geometric representation of the cortical regions is a fundamental task for cortical shape analysis and landmark extraction. However, a significant challenge has arisen due to the highly variable, convoluted cortical folding patterns. In this paper, we propose a novel topological graph representation for automatic sulcal curve extraction (TRACE). In practice, the reconstructed surface suffers from noise influences introduced during image acquisition/surface reconstruction. In the presence of noise on the surface, TRACE determines stable sulcal fundic regions by employing the line simplification method that prevents the sulcal folding pattern from being significantly smoothed out. The sulcal curves are then traced over the connected graph in the determined regions by the Dijkstra’s shortest path algorithm. For validation, we used state-of-the-art surface reconstruction pipelines on a reproducibility dataset. The experimental results showed higher reproducibility and robustness to noise in TRACE than the existing method (Li et al. 2010) with over 20% relative improvement in error for both surface reconstruction pipelines. In addition, the extracted sulcal curves by TRACE were well-aligned with manually delineated primary sulcal curves. We also provided a choice of parameters to control quality of the extracted sulcal curves and showed the influences of the parameter selection on the resulting curves.

- [Lyu I, Kim SH, Girault JB, Gilmore JH, Styner MA. A cortical shape-adaptive approach to local gyrification index. Med Image Anal. 2018;48:244‐258. doi:10.1016/j.media.2018.06.009 ](https://pubmed.ncbi.nlm.nih.gov/29990689/) The amount of cortical folding, or gyrification, is typically measured within local cortical regions covered by an equidistant geodesic or nearest neighborhood-ring kernel. However, without careful design, such a kernel can easily cover multiple sulcal and gyral regions that may not be functionally related. Furthermore, this can result in smoothing out details of cortical folding, which consequently blurs local gyrification measurements. In this paper, we propose a novel kernel shape to locally quantify cortical gyrification within sulcal and gyral regions. We adapt wavefront propagation to generate a spatially varying kernel shape that encodes cortical folding patterns: neighboring gyral crowns, sulcal fundi, and sulcal banks. For that purpose, we perform anisotropic wavefront propagation that runs fast along the gyral crowns and sulcal fundi by solving a static Hamilton-Jacobi partial differential equation. The resulting kernel adaptively elongates along gyral crowns and sulcal fundi, while keeping a uniform shape over flat regions like the sulcal banks. We then measure local gyrification within the proposed spatially varying kernel. The experimental results show that the proposed kernel-based gyrification measure achieves a higher reproducibility than the conventional method in a multi-scan dataset. We further apply the proposed kernel to a brain development study in the early postnatal phase from neonate to 2 years of age. In this study we find that our kernel yields both positive and negative associations of gyrification with age, whereas the conventional method only captures positive associations. In general, our method yields sharper and more detailed statistical maps that associate cortical folding with sex and gestational age.

- [Lyu I, Kang H, Woodward ND, Landman BA. Sulcal Depth-based Cortical Shape Analysis in Normal Healthy Control and Schizophrenia Groups. Proc SPIE Int Soc Opt Eng. 2018;10574:1057402. doi:10.1117/12.2293275](https://pubmed.ncbi.nlm.nih.gov/29887663/) Sulcal depth is an important marker of brain anatomy in neuroscience/neurological function. Previously, sulcal depth has been explored at the region-of-interest (ROI) level to increase statistical sensitivity to group differences. In this paper, we present a fully automated method that enables inferences of ROI properties from a sulcal region-focused perspective consisting of two main components: 1) sulcal depth computation and 2) sulcal curve-based refined ROIs. In conventional statistical analysis, the average sulcal depth measurements are employed in several ROIs of the cortical surface. However, taking the average sulcal depth over the full ROI blurs overall sulcal depth measurements which may result in reduced sensitivity to detect sulcal depth changes in neurological and psychiatric disorders. To overcome such a blurring effect, we focus on sulcal fundic regions in each ROI by filtering out other gyral regions. Consequently, the proposed method results in more sensitive to group differences than a traditional ROI approach. In the experiment, we focused on a cortical morphological analysis to sulcal depth reduction in schizophrenia with a comparison to the normal healthy control group. We show that the proposed method is more sensitivity to abnormalities of sulcal depth in schizophrenia; sulcal depth is significantly smaller in most cortical lobes in schizophrenia compared to healthy controls (p < 0.05).

- [Kim SH, Lyu I, Fonov VS, et al. Development of cortical shape in the human brain from 6 to 24months of age via a novel measure of shape complexity. Neuroimage. 2016;135:163‐176. doi:10.1016/j.neuroimage.2016.04.053](https://pubmed.ncbi.nlm.nih.gov/27150231/) The quantification of local surface morphology in the human cortex is important for examining population differences as well as developmental changes in neurodegenerative or neurodevelopmental disorders. We propose a novel cortical shape measure, referred to as the ‘shape complexity index’ (SCI), that represents localized shape complexity as the difference between the observed distributions of local surface topology, as quantified by the shape index (SI) measure, to its best fitting simple topological model within a given neighborhood. We apply a relatively small, adaptive geodesic kernel to calculate the SCI. Due to the small size of the kernel, the proposed SCI measure captures fine differences of cortical shape. With this novel cortical feature, we aim to capture comparatively small local surface changes that capture a) the widening versus deepening of sulcal and gyral regions, as well as b) the emergence and development of secondary and tertiary sulci. Current cortical shape measures, such as the gyrification index (GI) or intrinsic curvature measures, investigate the cortical surface at a different scale and are less well suited to capture these particular cortical surface changes. In our experiments, the proposed SCI demonstrates higher complexity in the gyral/sulcal wall regions, lower complexity in wider gyral ridges and lowest complexity in wider sulcal fundus regions. In early postnatal brain development, our experiments show that SCI reveals a pattern of increased cortical shape complexity with age, as well as sexual dimorphisms in the insula, middle cingulate, parieto-occipital sulcal and Broca’s regions. Overall, sex differences were greatest at 6months of age and were reduced at 24months, with the difference pattern switching from higher complexity in males at 6months to higher complexity in females at 24months. This is the first study of longitudinal, cortical complexity maturation and sex differences, in the early postnatal period from 6 to 24months of age with fine scale, cortical shape measures. These results provide information that complement previous studies of gyrification index in early brain development.

