# tractoflow

TractoFlow [1] pipeline is developed by the Sherbrooke Connectivity Imaging Lab (SCIL) in order to process diffusion MRI dataset from the raw data to the tractography. The pipeline is based on Nextflow [2]. This pipeline is optimized for healthy human adults.

TractoFlow pipeline consist of 23 different steps : 14 steps for the diffusion weighted image (DWI) processing and 8 steps for the T1 weighted image processing. See https://tractoflow-documentation.readthedocs.io/en/latest/index.html and [1] for more details.

## Requirements/Prerequisites

- dtiqa/prequal pipeline

## Version Information

- Current Version: tractoflow_v1.0.1
- Processor Name: tractoflow_v1.0.1_processor.yaml
- Singularity Recipe and Code: https://github.com/MASILab/tractoflow_spider
- SHA256 Hash: tractoflow_v1.0.0.simg (SHA256 cf5ecec0b1fe04b4daae31ba333ad04b35c6281319d75f7fa4a54eb0071bc947)

## Input Assumptions and Parameters Choice

1. The diffusion has been preprocessed using the dtiQA_v7 pipeline.
2. The parameters dti_shells and fodf_shells must be chosen according to each project’s sequence. It can be single-shell or multi-shell.
3. The acquisition is adequate for tensor reconstruction, 800 < BVAL < 1200, with at least 12 directions.
4. The acquistion is adequate for fODF reconstruction, 800 < BVAL < 3000, with at least 32 directions.
5. The parameters sh_order (default: 8) is the order of spherical harmonics used for fODF. If your fodf_shells has less than 45 directions, used 6.
6. pft_mask_type and local_mask_type (default: wm) defines the initialization “tissue” for tractography. If there is a chance for lesions and tissue segmentation is likely to fail, we recommand switching to fa.
7. pft_seed and local_seed (default: 10) define the number of streamlines to initialize per voxel of white matter (or fa).
8. If tracking is not desired or will be performed outside of the spider, use the smallest values possible (1).
9. The algo parameter is the choice of tractography algorithm (probabilistic). It is recommanded for most situation, if you want deterministic tractography switch to det.

## Inputs

- dwmri.nii.gz (from dtiQA – PREPROCESSED)
- dwmri.bval (from dtiQA – PREPROCESSED)
- dwmri.bvec (from dtiQA – PREPROCESSED)
- t1.nii.gz (from DICOM conversion)

## Parameters

- sh_order: 8
- dti_shells: “0 1000”
- fodf_shells: “0 1000”
- pft_seed: 10
- pft_mask_type: wm
- local_seed: 10
- local_mask_type: wm
- algo: prob

## Outputs

**Reporting**

- readme.txt
- report.html
- report.pdf

**DWI**

- dwi.bval
- dwi.bvec
- dwi_resampled.nii.gz
- b0_mask_resampled.nii.gz
- b0_resampled.nii.gz

**DTI_mtrics**

- md.nii.gz
- rd.nii.gz
- ad.nii.gz
- rgb.nii.gz
- tensor.nii.gz
- evals_e1.nii.gz
- evecs_v1.nii.gz

**FODF_metrics**

- fodf.nii.gz
- peaks.nii.gz
- nufo.nii.gz
- afd_max.nii.gz
- afd_sum.nii.gz
- afd_total.nii.gz

**Register_T1w**

- t1_mask_warped.nii.gz
- t1_warped.nii.gz
- output0GenericAffine.mat
- output1InverseWarp.nii.gz
- output1Warp.nii.gz

**Tissue Segmentation**

- mask_csf.nii.gz
- mask_gm.nii.gz
- mask_wm.nii.gz
- map_csf.nii.gz
- map_gm.nii.gz
- map_wm.nii.gz

**Tractography Masks**

- map_exclude.nii.gz
- map_include.nii.gz
- interface.nii.gz
- local_seeding_mask.nii.gz
- local_tracking_mask.nii.gz
- pft_seeding_mask.nii.gz

**Tracking**

- local.trk
- pft.trk

## Usage

```
singularity run
--home $JOBDIR
--containall
--cleanenv
--bind $INDIR:/INPUTS
--bind  $OUTDIR:/OUTPUTS
--bind $JOBDIR:/TMP
{container_path}
{subject}
{session}
{t1_file}
{dti_nifti}
{dti_bval}
{dti_bvec}
{sh_order}
{dti_shells}
{fodf_shells}
{pft_seed}
{pft_mask_type}
{local_seed}
{local_mask_type}
{algo}
```

## References

- [Theaud, G., Houde, J.-C., Boré, A., Rheault, F., Morency, F., Descoteaux, M., “TractoFlow: A robust, efficient and reproducible diffusion MRI pipeline leveraging Nextflow & Singularity”, NeuroImage (2020).](https://www.sciencedirect.com/science/article/pii/S105381192030375X)
Diffusion MRI tractography processing pipeline requires a large number of steps (typically 20+ steps). If parameters of these steps, number of threads, and random seed generators are not carefully controlled, the resulting tractography can easily be non-reproducible and non-replicable, even in test-test experiments. To handle these issues, we developed TractoFlow. TractoFlow is fully automatic from raw diffusion weighted images to tractography. The pipeline also outputs classical diffusion tensor imaging measures and several fiber orientation distribution function measures. TractoFlow supports the recent Brain Imaging Data Structure (BIDS) format as input and is based on two engines: Nextflow and Singularity. In this work, the TractoFlow pipeline is evaluated on three databases and shown to be efficient and reproducible from 98% to 100%, depending on parameter choices. Moreover, it is easy to use for non-technical users, with little to no installation requirements. TractoFlow is publicly available for academic research and is an important step forward for better structural brain connectivity mapping.

- [Paolo Di Tommaso, et al. “Nextflow enables reproducible computational workflows.”, Nature Biotechnology 35, 316-319 (2017)](https://pubmed.ncbi.nlm.nih.gov/28398311/)

- [Garyfallidis, E., Brett, M., Amirbekian, B., Rokem, A., Van Der Walt, S., Descoteaux, M., Nimmo-Smith, I., “Dipy, a library for the analysis of diffusion mri data.”, Frontiers in neuroinformatics (2014) 8, 8.](https://pubmed.ncbi.nlm.nih.gov/24600385/)
Diffusion Imaging in Python (Dipy) is a free and open source software project for the analysis of data from diffusion magnetic resonance imaging (dMRI) experiments. dMRI is an application of MRI that can be used to measure structural features of brain white matter. Many methods have been developed to use dMRI data to model the local configuration of white matter nerve fiber bundles and infer the trajectory of bundles connecting different parts of the brain. Dipy gathers implementations of many different methods in dMRI, including: diffusion signal pre-processing; reconstruction of diffusion distributions in individual voxels; fiber tractography and fiber track post-processing, analysis and visualization. Dipy aims to provide transparent implementations for all the different steps of dMRI analysis with a uniform programming interface. We have implemented classical signal reconstruction techniques, such as the diffusion tensor model and deterministic fiber tractography. In addition, cutting edge novel reconstruction techniques are implemented, such as constrained spherical deconvolution and diffusion spectrum imaging (DSI) with deconvolution, as well as methods for probabilistic tracking and original methods for tractography clustering. Many additional utility functions are provided to calculate various statistics, informative visualizations, as well as file-handling routines to assist in the development and use of novel techniques. In contrast to many other scientific software projects, Dipy is not being developed by a single research group. Rather, it is an open project that encourages contributions from any scientist/developer through GitHub and open discussions on the project mailing list. Consequently, Dipy today has an international team of contributors, spanning seven different academic institutions in five countries and three continents, which is still growing.

- [Tournier, J. D., Smith, R. E., Raffelt, D. A., Tabbara, R., Dhollander, T., Pietsch, M., & Connelly, A., “MRtrix3: A fast, flexible and open software framework for medical image processing and visualisation.”, Neuroimage (2020).](https://www.sciencedirect.com/science/article/abs/pii/S1053811919307281)
MRtrix3 is an open-source, cross-platform software package for medical image processing, analysis and visualisation, with a particular emphasis on the investigation of the brain using diffusion MRI. It is implemented using a fast, modular and flexible general-purpose code framework for image data access and manipulation, enabling efficient development of new applications, whilst retaining high computational performance and a consistent command-line interface between applications. In this article, we provide a high-level overview of the features of the MRtrix3 framework and general-purpose image processing applications provided with the software.

- [Avants, B.B., Tustison, N., Song, G., “Advanced normalization tools (ants).” Insight J (2009) 2, 1-35.](http://scil.dinf.usherbrooke.ca/static/website/courses/imn530/ants.pdf)

- [Jenkinson, M., Beckmann, C.F., Behrens, T.E., Woolrich, M.W., Smith, S.M., “Fsl.” Neuroimage 62 (2012), 782-790.](https://pubmed.ncbi.nlm.nih.gov/21979382/)
FSL (the FMRIB Software Library) is a comprehensive library of analysis tools for functional, structural and diffusion MRI brain imaging data, written mainly by members of the Analysis Group, FMRIB, Oxford. For this NeuroImage special issue on “20 years of fMRI” we have been asked to write about the history, developments and current status of FSL. We also include some descriptions of parts of FSL that are not well covered in the existing literature. We hope that some of this content might be of interest to users of FSL, and also maybe to new research groups considering creating, releasing and supporting new software packages for brain image analysis.
