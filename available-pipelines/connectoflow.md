# connectoflow

Connectoflow [1] is Nextflow [2] pipeline to generate Connectomics [3,4] matrices from tractography data. The key steps in this version of Connectoflow are:

- Decompose: This step performs the parcel-to-parcel decomposition of the tractogram. It includes streamline-cutting operations to ensure streamlines have terminations in the provided atlas. Moreover, connection-wise cleaning processes that remove loops, discard spurious streamlines and discard incoherent curvatures are used to remove as many false positives as possible [5].
- COMMIT: To further decrease the number of invalid streamlines and assign a quantitative weight to each streamline, Convex Optimization Modeling for Micro-structure Informed Tractography (COMMIT) [6,7] is used. This not only allows the removal of aberrant or spurious streamlines, but it was shown to increase reproducibility of connectivity measures by being more robust to various tractography biases.
- AFD: Apparent Fiber Density (AFD) [8,9] is subsequently computed connection-wise using streamline orientations (fixel), which can be computationally burdensome if done on every pairwise connection of the connectome a posteriori. This step will provide a AFD-weighted connectivity matrix.

## Requirements/Prerequisites

- Slant pipeline
- tractoflow pipeline

**NOTE: Connectoflow previous version 1.0.0 had an error in the way some metrics were computed that led to matrices (like FA/MD) to be scaled wrong.**

Some groups required customization of atlases (other than SLANT) so a new parameter was needed to avoid needing a singularity per project.

## Version Information

- Current Version: connectoflow_v2.1.0
- Processor Name: connectoflow_v2.1.0_processor.yaml
- Singularity Recipe and Code: https://github.com/VUIIS/yaml_processors/blob/running_processors/connectoflow_v2.1.0_processor.yaml
- SHA256 Hash: connectoflow_v2.1.0.sif (SHA256 b73831a84ed2bfa8c195c305b77dfd853d51217992c91caa9d8d77ce86622f1a)

## Input Assumptions and Parameters Choice

Tractogram from Tractoflow should have at least 1M-2M streamlines Connectoflow is optimized for probabilistic tractography Connectoflow is robust to lesions/tumors IF the tractography was adapted for the situation AND Slant parcellations is valid This pipeline does not perform any statistical analysis, this should be planned separately beforehand.

**INPUTS**

- t1.nii.gz (from Slant)
- labels.nii.gz (from Slant)
- dwi_resampled.nii.gz (from Tractoflow)
- dwi_resampled.nii.gz (from Tractoflow)
- dwi.bval (from Tractoflow)
- dwi.bvec (from Tractoflow)
- fodf.nii.gz (from Tractoflow)
- peaks.nii.gz (from Tractoflow)
- fodf.nii.gz (from Tractoflow)
- output0GenericAffine.mat (from Tractoflow)
- output1Warp.nii.gz (from Tractoflow)
- fa.nii.gz (from Tractoflow)
- md.nii.gz (from Tractoflow)
- rd.nii.gz (from Tractoflow)
- ad.nii.gz (from Tractoflow)
- nufo.nii.gz (from Tractoflow)
- afd_total.nii.gz (from Tractoflow)
- afd_sum.nii.gz (from Tractoflow)
- afd_max.nii.gz (from Tractoflow)
- ensemble.trk (from Tractoflow)

**OUTPUTS**

- Reporting
  - report.html
  - report.pdf
- Connectivity Matrices
  - *.npy
- MNI Space Data
  - mni_icbm152_nlin_asym_09c_t1_masked.nii.gz (template)
  - labels_warped_mni_int16.nii.gz
  - t1_mni.nii.gz
  - decompose_warped_mni.h5
- Transforms to MNI
  - output0GenericAffine.mat
  - output1Warp.nii.gz
  - output1InverseWarp.nii.gz

## References

- [Rheault, Francois, et al. “Connectoflow: A cutting-edge Nextflow pipeline for structural connectomics”, ISMRM 2021 Proceedings, #710.](https://www.researchgate.net/publication/351662030_Connectoflow_A_cutting-edge_Nextflow_pipeline_for_structural_connectomics)
Tractography involves complicated processing and connectomics include even more complexity. To facilitate structural connectome reconstructionwe present: Connectoflow. Connectoflow requires simple inputs, has simple options and provides simple outputs, all with cutting-edge processing.By leveraging the simplicity of Nextflow and Docker/Singularity, Connectoflow is robust and efficient. By combining Tractoflow with Connectoflow,one can go from raw DW-images to structural connectomes in a few simplified steps. The proposed pipeline innovates by including connection-wisecleaning/filtering, provides connection weights that go beyond streamline count (COMMIT) as well as advanced connection-wise metrics (similarityand AFD)

- [Di Tommaso, Paolo, et al. “Nextflow enables reproducible computational workflows.”, Nature biotechnology 35.4 (2017): 316-319.](https://pubmed.ncbi.nlm.nih.gov/28398311/)

- [Sotiropoulos, Stamatios N., and Andrew Zalesky. “Building connectomes using diffusion MRI: why, how and but.”, NMR in Biomedicine 32.4 (2019): e3752.](https://pubmed.ncbi.nlm.nih.gov/28654718/)
Why has diffusion MRI become a principal modality for mapping connectomes in vivo? How do different image acquisition parameters, fiber tracking algorithms and other methodological choices affect connectome estimation? What are the main factors that dictate the success and failure of connectome reconstruction? These are some of the key questions that we aim to address in this review. We provide an overview of the key methods that can be used to estimate the nodes and edges of macroscale connectomes, and we discuss open problems and inherent limitations. We argue that diffusion MRI-based connectome mapping methods are still in their infancy and caution against blind application of deep white matter tractography due to the challenges inherent to connectome reconstruction. We review a number of studies that provide evidence of useful microstructural and network properties that can be extracted in various independent and biologically relevant contexts. Finally, we highlight some of the key deficiencies of current macroscale connectome mapping methodologies and motivate future developments.

- [Yeh, Chun-Hung, et al. “Mapping structural connectivity using diffusion MRI: challenges and opportunities.”, Journal of Magnetic Resonance Imaging (2020).](https://pubmed.ncbi.nlm.nih.gov/32557893/)
Diffusion MRI-based tractography is the most commonly-used technique when inferring the structural brain connectome, i.e., the comprehensive map of the connections in the brain. The utility of graph theory-a powerful mathematical approach for modeling complex network systems-for analyzing tractography-based connectomes brings important opportunities to interrogate connectome data, providing novel insights into the connectivity patterns and topological characteristics of brain structural networks. When applying this framework, however, there are challenges, particularly regarding methodological and biological plausibility. This article describes the challenges surrounding quantitative tractography and potential solutions. In addition, challenges related to the calculation of global network metrics based on graph theory are discussed.Evidence Level: 5Technical Efficacy: Stage 1.

- [Zhang, Zhengwu, et al. “Mapping population-based structural connectomes.”, NeuroImage 172 (2018): 130-145.](https://pubmed.ncbi.nlm.nih.gov/29355769/)
Advances in understanding the structural connectomes of human brain require improved approaches for the construction, comparison and integration of high-dimensional whole-brain tractography data from a large number of individuals. This article develops a population-based structural connectome (PSC) mapping framework to address these challenges. PSC simultaneously characterizes a large number of white matter bundles within and across different subjects by registering different subjects’ brains based on coarse cortical parcellations, compressing the bundles of each connection, and extracting novel connection weights. A robust tractography algorithm and streamline post-processing techniques, including dilation of gray matter regions, streamline cutting, and outlier streamline removal are applied to improve the robustness of the extracted structural connectomes. The developed PSC framework can be used to reproducibly extract binary networks, weighted networks and streamline-based brain connectomes. We apply the PSC to Human Connectome Project data to illustrate its application in characterizing normal variations and heritability of structural connectomes in healthy subjects.

- [Daducci, Alessandro, et al. “COMMIT: convex optimization modeling for microstructure informed tractography.”, IEEE transactions on medical imaging 34.1 (2014): 246-257.](https://pubmed.ncbi.nlm.nih.gov/25167548/)
Tractography is a class of algorithms aiming at in vivo mapping the major neuronal pathways in the white matter from diffusion magnetic resonance imaging (MRI) data. These techniques offer a powerful tool to noninvasively investigate at the macroscopic scale the architecture of the neuronal connections of the brain. However, unfortunately, the reconstructions recovered with existing tractography algorithms are not really quantitative even though diffusion MRI is a quantitative modality by nature. As a matter of fact, several techniques have been proposed in recent years to estimate, at the voxel level, intrinsic microstructural features of the tissue, such as axonal density and diameter, by using multicompartment models. In this paper, we present a novel framework to reestablish the link between tractography and tissue microstructure. Starting from an input set of candidate fiber-tracts, which are estimated from the data using standard fiber-tracking techniques, we model the diffusion MRI signal in each voxel of the image as a linear combination of the restricted and hindered contributions generated in every location of the brain by these candidate tracts. Then, we seek for the global weight of each of them, i.e., the effective contribution or volume, such that they globally fit the measured signal at best. We demonstrate that these weights can be easily recovered by solving a global convex optimization problem and using efficient algorithms. The effectiveness of our approach has been evaluated both on a realistic phantom with known ground-truth and in vivo brain data. Results clearly demonstrate the benefits of the proposed formulation, opening new perspectives for a more quantitative and biologically plausible assessment of the structural connectivity of the brain.

- [Schiavi, Simona, et al. “A new method for accurate in vivo mapping of human brain connections using microstructural, and anatomical information.” Science advances 6.31 (2020): eaba8245.](https://www.science.org/doi/10.1126/sciadv.aba8245)
Diffusion magnetic resonance imaging is a noninvasive imaging modality that has been extensively used in the literature to study the neuronal architecture of the brain in a wide range of neurological conditions using tractography. However, recent studies highlighted that the anatomical accuracy of the reconstructions is inherently limited and challenged its appropriateness. Several solutions have been proposed to tackle this issue, but none of them proved effective to overcome this fundamental limitation. In this work, we present a novel processing framework to inject into the reconstruction problem basic prior knowledge about brain anatomy and its organization and evaluate its effectiveness using both simulated and real human brain data. Our results indicate that our proposed method dramatically increases the accuracy of the estimated brain networks and, thus, represents a major step forward for the study of connectivity.

- [Raffelt, David A., et al. “Investigating white matter fibre density and morphology using fixel-based analysis.”, Neuroimage 144 (2017): 58-73](https://pubmed.ncbi.nlm.nih.gov/27639350/)
Voxel-based analysis of diffusion MRI data is increasingly popular. However, most white matter voxels contain contributions from multiple fibre populations (often referred to as crossing fibres), and therefore voxel-averaged quantitative measures (e.g. fractional anisotropy) are not fibre-specific and have poor interpretability. Using higher-order diffusion models, parameters related to fibre density can be extracted for individual fibre populations within each voxel (‘fixels’), and recent advances in statistics enable the multi-subject analysis of such data. However, investigating within-voxel microscopic fibre density alone does not account for macroscopic differences in the white matter morphology (e.g. the calibre of a fibre bundle). In this work, we introduce a novel method to investigate the latter, which we call fixel-based morphometry (FBM). To obtain a more complete measure related to the total number of white matter axons, information from both within-voxel microscopic fibre density and macroscopic morphology must be combined. We therefore present the FBM method as an integral piece within a comprehensive fixel-based analysis framework to investigate measures of fibre density, fibre-bundle morphology (cross-section), and a combined measure of fibre density and cross-section. We performed simulations to demonstrate the proposed measures using various transformations of a numerical fibre bundle phantom. Finally, we provide an example of such an analysis by comparing a clinical patient group to a healthy control group, which demonstrates that all three measures provide distinct and complementary information. By capturing information from both sources, the combined fibre density and cross-section measure is likely to be more sensitive to certain pathologies and more directly interpretable.

- [Dhollander, Thijs, et al. “Fixel-based Analysis of Diffusion MRI: Methods, Applications, Challenges and Opportunities.” (2020).](https://www.sciencedirect.com/science/article/pii/S1053811921000896)
Language is the most commonly described lateralised cognitive function, relying more on the left hemisphere compared to the right hemisphere in over 90% of the population. Most research examining the structure-function relationship of language lateralisation only included people showing a left language hemisphere dominance. In this work, we applied a state-of-the-art “fixel-based” analysis approach, allowing statistical analysis of white matter micro- and macrostructure on a fibre-specific level in a sample of participants with left and right language dominance (LLD and RLD). Both groups showed a similar extensive pattern of white matter lateralisation including a comparable leftwards lateralisation of the arcuate fasciculus, regardless of their functional language lateralisation. These results suggest that lateralisation of language functioning and the arcuate fasciculus are driven by independent biases. Finally, a significant group difference of lateralisation was detected in the forceps minor, with a leftwards lateralisation in LLD and rightwards lateralisation for the RLD group.
