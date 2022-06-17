# Connectivity Atlases Flow

This pipeline facilitates the creation of atlases for Connectoflow [1]. It creates atlases from the Freesurfer output: Brainnetome [2], Glasser [3], Schaefer [4], Lausanne multi-scales [5] and lobes. All atlases are free of WM and CSF labels, ready for connectomics. All output atlases have the following files associated with them:

- atlas_*_v4.nii.gz (parcellation as computed)
- atlas_*_v4_dilate.nii.gz (parcellation with cortical labels dilate into the WM)
- atlas_*_v4_LUT.json (Links the labels number to its name)
- atlas_*_v4_LUT.txt (Links the labels number to its name and color scheme for Freeview)
- atlas_*_v4_labels_list.txt (Contains the list of expected labels number)

## Version Information

- Current Version: connectivity_atlas_flow_v2
- Processor Name: connectivity_atlas_flow_v2_processor.yaml
- Singularity Recipe and Code: https://github.com/MASILab/connectivity_atlases_flow_spider
- SHA256 Hash:connectivity_atlas_flow_spider_v3.sif (SHA256 a7ee353d5d410b51d3daef430d762da8f0d80278c17918284251449f29a35d4f)

## Assumptions and User Guide

**Input Assumptions and Parameters Choice**

1. The input T1w image should not have been skull strip.
2. If the goal is to use this pipeline with Connectoflow, they need the same T1w as input.

**Inputs** 

- t1.nii.gz (Same as the one given to Tractoflow)

**Outputs**

- Reporting
  - report.html
  - report.pdf
- Atlases
  - freesurfer.[nii.gz,txt,json]
  - brainnetome.[nii.gz,txt,json]
  - glasser.[nii.gz,txt,json]
  - lobes.[nii.gz,txt,json]
  - schaefer_100.[nii.gz,txt,json]
  - schaefer_200.[nii.gz,txt,json]
  - schaefer_400.[nii.gz,txt,json]
  - lausanne_2008_scale_1.[nii.gz,txt,json]
  - lausanne_2008_scale_2.[nii.gz,txt,json]
  - lausanne_2008_scale_3.[nii.gz,txt,json]
  - lausanne_2008_scale_4.[nii.gz,txt,json]
  - lausanne_2008_scale_5.[nii.gz,txt,json]

## References

- [Rheault, Francois, et al. “Connectoflow: A cutting-edge Nextflow pipeline for structural connectomics”, ISMRM 2021 Proceedings, #710.](https://www.researchgate.net/publication/351662030_Connectoflow_A_cutting-edge_Nextflow_pipeline_for_structural_connectomics)
Tractography involves complicated processing and connectomics include even more complexity. To facilitate structural connectome reconstructionwe present: Connectoflow. Connectoflow requires simple inputs, has simple options and provides simple outputs, all with cutting-edge processing.By leveraging the simplicity of Nextflow and Docker/Singularity, Connectoflow is robust and efficient. By combining Tractoflow with Connectoflow,one can go from raw DW-images to structural connectomes in a few simplified steps. The proposed pipeline innovates by including connection-wisecleaning/filtering, provides connection weights that go beyond streamline count (COMMIT) as well as advanced connection-wise metrics (similarityand AFD)

- [Fan, Lingzhong, et al. “The human brainnetome atlas: a new brain atlas based on connectional architecture.”, Cerebral cortex 26.8 (2016): 3508-3526.](https://pubmed.ncbi.nlm.nih.gov/27230218/)
The human brain atlases that allow correlating brain anatomy with psychological and cognitive functions are in transition from ex vivo histology-based printed atlases to digital brain maps providing multimodal in vivo information. Many current human brain atlases cover only specific structures, lack fine-grained parcellations, and fail to provide functionally important connectivity information. Using noninvasive multimodal neuroimaging techniques, we designed a connectivity-based parcellation framework that identifies the subdivisions of the entire human brain, revealing the in vivo connectivity architecture. The resulting human Brainnetome Atlas, with 210 cortical and 36 subcortical subregions, provides a fine-grained, cross-validated atlas and contains information on both anatomical and functional connections. Additionally, we further mapped the delineated structures to mental processes by reference to the BrainMap database. It thus provides an objective and stable starting point from which to explore the complex relationships between structure, connectivity, and function, and eventually improves understanding of how the human brain works. The human Brainnetome Atlas will be made freely available for download at http://atlas.brainnetome.org, so that whole brain parcellations, connections, and functional data will be readily available for researchers to use in their investigations into healthy and pathological states.

- [Glasser, Matthew F., et al. “A multi-modal parcellation of human cerebral cortex.”, Nature 536.7615 (2016): 171-178.](https://www.nature.com/articles/nature18933)
Understanding the amazingly complex human cerebral cortex requires a map (or parcellation) of its major subdivisions, known as cortical areas. Making an accurate areal map has been a century-old objective in neuroscience. Using multi-modal magnetic resonance images from the Human Connectome Project (HCP) and an objective semi-automated neuroanatomical approach, we delineated 180 areas per hemisphere bounded by sharp changes in cortical architecture, function, connectivity, and/or topography in a precisely aligned group average of 210 healthy young adults. We characterized 97 new areas and 83 areas previously reported using post-mortem microscopy or other specialized study-specific approaches. To enable automated delineation and identification of these areas in new HCP subjects and in future studies, we trained a machine-learning classifier to recognize the multi-modal ‘fingerprint’ of each cortical area. This classifier detected the presence of 96.6% of the cortical areas in new subjects, replicated the group parcellation, and could correctly locate areas in individuals with atypical parcellations. The freely available parcellation and classifier will enable substantially improved neuroanatomical precision for studies of the structural and functional organization of human cerebral cortex and its variation across individuals and in development, aging, and disease.

- [Schaefer, Alexander, et al. “Local-global parcellation of the human cerebral cortex from intrinsic functional connectivity MRI.”, Cerebral cortex 28.9 (2018): 3095-3114.](https://pubmed.ncbi.nlm.nih.gov/28981612/)
A central goal in systems neuroscience is the parcellation of the cerebral cortex into discrete neurobiological “atoms”. Resting-state functional magnetic resonance imaging (rs-fMRI) offers the possibility of in vivo human cortical parcellation. Almost all previous parcellations relied on 1 of 2 approaches. The local gradient approach detects abrupt transitions in functional connectivity patterns. These transitions potentially reflect cortical areal boundaries defined by histology or visuotopic fMRI. By contrast, the global similarity approach clusters similar functional connectivity patterns regardless of spatial proximity, resulting in parcels with homogeneous (similar) rs-fMRI signals. Here, we propose a gradient-weighted Markov Random Field (gwMRF) model integrating local gradient and global similarity approaches. Using task-fMRI and rs-fMRI across diverse acquisition protocols, we found gwMRF parcellations to be more homogeneous than 4 previously published parcellations. Furthermore, gwMRF parcellations agreed with the boundaries of certain cortical areas defined using histology and visuotopic fMRI. Some parcels captured subareal (somatotopic and visuotopic) features that likely reflect distinct computational units within known cortical areas. These results suggest that gwMRF parcellations reveal neurobiologically meaningful features of brain organization and are potentially useful for future applications requiring dimensionality reduction of voxel-wise fMRI data. Multiresolution parcellations generated from 1489 participants are publicly available (https://github.com/ThomasYeoLab/CBIG/tree/master/stable_projects/brain_parcellation/Schaefer2018_LocalGlobal).

- [Tourbier, Sebastien et al. “Multi-scale-brain-parcellator-a-bids-app-for-the-lausanne-connectome-parcellation”, OHBM 2019 Annual Meeting.](https://cibm.ch/research/publications/multi-scale-brain-parcellator-a-bids-app-for-the-lausanne-connectome-parcellation/)
Connectome Mapper (CMP), part of the Connectome Mapping Toolkit (CMTK), is an open-source software which implements full anatomical, diffusion and resting state functional MRI processing pipelines to map connectivity matrices from raw Diffusion/T1/T2 and BOLD data (Daducci 2012). In parallel of its third release (connectome-mapper-3.readthedocs.io), we developed an independent tool: the Multi-Scale Brain Parcellator. This tool, which takes BIDS structured datasets as input, implements a 5-scale brain gray matter parcellation (Cammoun 2012) derived from the Desikan-Killiany atlas (Desikan 2004) and extended with new structures including a subdivision of the thalamus into 7 nuclei, the hippocampus into 12 subfields and the brainstem into 4 sub-structures. Such a brain parcellation can serve many add on applications such as volumetry and definition of regions of interest for tractography or functional connectivity analysis.
