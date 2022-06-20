# rbx_flow

RecobundlesX is a multi-atlas, multi-parameters version of Recobundles [1, 2]. It is optimized for whole brain coverage using 39 major well-known white matter pathways. The atlas is a customized population average from 20 UKBioBank [3] and 20 Human Connectome Project [4] datasets co-registered to MNI152 space.

This atlas was made to cover as much spatial extend as possible and explore as much shape variability as possible. Recobundles is when run 27 times with bundle-specific paramters and the results of each execution are used in a majority-vote approach. This is inspired from the state-of-the-art in medical images segmentation (before machine-learning) [5,6].

Then, a shape-based pruning is applied to each bundle to remove inconsistent or spurious streamlines (outliers) [7]. See https://zenodo.org/record/4630660# for more details.

## Requirements/Prerequisites

- tractoflow pipeline

RBx-Flow version 1.0.0 has a crash at report (pdf) creation due to missing bundles when some are not saved by the pipeline. Minor addition to check if files exist before trying to take a screenshot. I would consider that a patch, no need to rerun past datasets (could be v1.1 instead of v2)

## Version Information

- Current Version: rbx_flow_v1.1.0
- Processor Name: rbx_flow_v1.1.0_processor.yaml
- Singularity Recipe and Code: https://github.com/VUIIS/yaml_processors/blob/running_processors/rbx_flow_v1.1.0_processor.yaml
- SHA256 Hash: rbx_flow_v1.1.0.simg (SHA256 ba311d03e12ebb9e11172b61ab2d5602a49e563ed213215e9759079e489f780f)

## Input Assumptions and Parameter Choice

Tractogram from Tractoflow should have at least 1M-2M streamlines RecobundlesX is optimized for probabilistic tractography RecobundlesX is robust to lesions/tumors IF the tractography was adapted for the situation nb_run is between 1 and 27 vote_ratio is between 0 and 1

## Inputs

- fa.nii.gz (from Tractoflow)
- local_tracking.trk (from Tractoflow)
- pft_tracking.trk (from Tractoflow)

## Parameters

- nb_run: 27
- vote_ratio: 0.5

## Outputs

**Reporting**

- report.html
- report.pdf

**Bundles**

- *_cleaned.trk

**Centroids**

- *_centroids.trk

## References

- [Garyfallidis, Eleftherios, et al. “Recognition of white matter bundles using local and global streamline-based registration and clustering.” NeuroImage 170 (2018): 283-295.](https://pubmed.ncbi.nlm.nih.gov/28712994/)
Virtual dissection of diffusion MRI tractograms is cumbersome and needs extensive knowledge of white matter anatomy. This virtual dissection often requires several inclusion and exclusion regions-of-interest that make it a process that is very hard to reproduce across experts. Having automated tools that can extract white matter bundles for tract-based studies of large numbers of people is of great interest for neuroscience and neurosurgical planning. The purpose of our proposed method, named RecoBundles, is to segment white matter bundles and make virtual dissection easier to perform. This can help explore large tractograms from multiple persons directly in their native space. RecoBundles leverages latest state-of-the-art streamline-based registration and clustering to recognize and extract bundles using prior bundle models. RecoBundles uses bundle models as shape priors for detecting similar streamlines and bundles in tractograms. RecoBundles is 100% streamline-based, is efficient to work with millions of streamlines and, most importantly, is robust and adaptive to incomplete data and bundles with missing components. It is also robust to pathological brains with tumors and deformations. We evaluated our results using multiple bundles and showed that RecoBundles is in good agreement with the neuroanatomical experts and generally produced more dense bundles. Across all the different experiments reported in this paper, RecoBundles was able to identify the core parts of the bundles, independently from tractography type (deterministic or probabilistic) or size. Thus, RecoBundles can be a valuable method for exploring tractograms and facilitating tractometry studies.

- [Rheault, François. “Analyse et reconstruction de faisceaux de la matière blanche.” Computer Science (Université de Sherbrooke) (2020), https://savoirs.usherbrooke.ca/handle/11143/17255](https://www.usherbrooke.ca/actualites/evenements/soutenances-de-these/details/42241)
Diffusion magnetic resonance imaging and tractography are frequently used for the study of the structural connectivity of the brain. These methods are very useful for exploring the links between the organization of white matter and neurodegenerative disorders such as multiple sclerosis or Alzheimer’s or for neurosurgical planning. This medical imaging modality could lead to valuable biomarkers that make it possible to differentiate groups suffering from pathologies versus control groups, to make prediction, aid in diagnosis or simply to advance our knowledge in neuroanatomy.
This thesis defense focuses more particularly on the reconstruction of white matter beams as well as their analyzes. First, a brief introduction to diffusion magnetic resonance imaging and neuroimaging will be presented, to then continue with the specific objectives of this thesis. The major themes addressed during this presentation are related to attempts to improve the reconstruction of white matter beams, to virtual dissection (manual or automatic) of white matter beams and to the evaluation of the variability of the white matter. virtual dissection (manual or automatic) of white matter bundles.
The general objective of this work is to improve and facilitate the use of tractography in the context of research, but also for clinical applications.

- [Sudlow, Cathie, et al. “UK biobank: an open access resource for identifying the causes of a wide range of complex diseases of middle and old age.” Plos med 12.3 (2015): e1001779.](https://pubmed.ncbi.nlm.nih.gov/25826379/)
Cathie Sudlow and colleagues describe the UK Biobank, a large population-based prospective study, established to allow investigation of the genetic and non-genetic determinants of the diseases of middle and old age.

- [Van Essen, David C., et al. “The WU-Minn human connectome project: an overview.” Neuroimage 80 (2013): 62-79.](https://www.sciencedirect.com/science/article/abs/pii/S1053811913005351)
The Human Connectome Project consortium led by Washington University, University of Minnesota, and Oxford University is undertaking a systematic effort to map macroscopic human brain circuits and their relationship to behavior in a large population of healthy adults. This overview article focuses on progress made during the first half of the 5-year project in refining the methods for data acquisition and analysis. Preliminary analyses based on a finalized set of acquisition and preprocessing protocols demonstrate the exceptionally high quality of the data from each modality. The first quarterly release of imaging and behavioral data via the ConnectomeDB database demonstrates the commitment to making HCP datasets freely accessible. Altogether, the progress to date provides grounds for optimism that the HCP datasets and associated methods and software will become increasingly valuable resources for characterizing human brain connectivity and function, their relationship to behavior, and their heritability and genetic underpinnings.

- [Iglesias, Juan Eugenio, and Mert R. Sabuncu. “Multi-atlas segmentation of biomedical images: a survey.” Medical image analysis 24.1 (2015): 205-219.](https://pubmed.ncbi.nlm.nih.gov/26201875/)
Multi-atlas segmentation (MAS), first introduced and popularized by the pioneering work of Rohlfing, et al. (2004), Klein, et al. (2005), and Heckemann, et al. (2006), is becoming one of the most widely-used and successful image segmentation techniques in biomedical applications. By manipulating and utilizing the entire dataset of “atlases” (training images that have been previously labeled, e.g., manually by an expert), rather than some model-based average representation, MAS has the flexibility to better capture anatomical variation, thus offering superior segmentation accuracy. This benefit, however, typically comes at a high computational cost. Recent advancements in computer hardware and image processing software have been instrumental in addressing this challenge and facilitated the wide adoption of MAS. Today, MAS has come a long way and the approach includes a wide array of sophisticated algorithms that employ ideas from machine learning, probabilistic modeling, optimization, and computer vision, among other fields. This paper presents a survey of published MAS algorithms and studies that have applied these methods to various biomedical problems. In writing this survey, we have three distinct aims. Our primary goal is to document how MAS was originally conceived, later evolved, and now relates to alternative methods. Second, this paper is intended to be a detailed reference of past research activity in MAS, which now spans over a decade (2003-2014) and entails novel methodological developments and application-specific solutions. Finally, our goal is to also present a perspective on the future of MAS, which, we believe, will be one of the dominant approaches in biomedical image segmentation.

- [Pipitone, Jon, et al. “Multi-atlas segmentation of the whole hippocampus and subfields using multiple automatically generated templates.” Neuroimage 101 (2014): 494-512.](https://pubmed.ncbi.nlm.nih.gov/24784800/)
  - **Introduction:** Advances in image segmentation of magnetic resonance images (MRI) have demonstrated that multi-atlas approaches improve segmentation over regular atlas-based approaches. These approaches often rely on a large number of manually segmented atlases (e.g. 30-80) that take significant time and expertise to produce. We present an algorithm, MAGeT-Brain (Multiple Automatically Generated Templates), for the automatic segmentation of the hippocampus that minimises the number of atlases needed whilst still achieving similar agreement to multi-atlas approaches. Thus, our method acts as a reliable multi-atlas approach when using special or hard-to-define atlases that are laborious to construct.
  - **Method:** MAGeT-Brain works by propagating atlas segmentations to a template library, formed from a subset of target images, via transformations estimated by nonlinear image registration. The resulting segmentations are then propagated to each target image and fused using a label fusion method. We conduct two separate Monte Carlo cross-validation experiments comparing MAGeT-Brain and basic multi-atlas whole hippocampal segmentation using differing atlas and template library sizes, and registration and label fusion methods. The first experiment is a 10-fold validation (per parameter setting) over 60 subjects taken from the Alzheimer’s Disease Neuroimaging Database (ADNI), and the second is a five-fold validation over 81 subjects having had a first episode of psychosis. In both cases, automated segmentations are compared with manual segmentations following the Pruessner-protocol. Using the best settings found from these experiments, we segment 246 images of the ADNI1:Complete 1Yr 1.5 T dataset and compare these with segmentations from existing automated and semi-automated methods: FSL FIRST, FreeSurfer, MAPER, and SNT. Finally, we conduct a leave-one-out cross-validation of hippocampal subfield segmentation in standard 3T T1-weighted images, using five high-resolution manually segmented atlases (Winterburn et al., 2013).
  - **Results:** In the ADNI cross-validation, using 9 atlases MAGeT-Brain achieves a mean Dice’s Similarity Coefficient (DSC) score of 0.869 with respect to manual whole hippocampus segmentations, and also exhibits significantly lower variability in DSC scores than multi-atlas segmentation. In the younger, psychosis dataset, MAGeT-Brain achieves a mean DSC score of 0.892 and produces volumes which agree with manual segmentation volumes better than those produced by the FreeSurfer and FSL FIRST methods (mean difference in volume: 80 mm(3), 1600 mm(3), and 800 mm(3), respectively). Similarly, in the ADNI1:Complete 1Yr 1.5 T dataset, MAGeT-Brain produces hippocampal segmentations well correlated (r>0.85) with SNT semi-automated reference volumes within disease categories, and shows a conservative bias and a mean difference in volume of 250 mm(3) across the entire dataset, compared with FreeSurfer and FSL FIRST which both overestimate volume differences by 2600 mm(3) and 2800 mm(3) on average, respectively. Finally, MAGeT-Brain segments the CA1, CA4/DG and subiculum subfields on standard 3T T1-weighted resolution images with DSC overlap scores of 0.56, 0.65, and 0.58, respectively, relative to manual segmentations.
  - **Conclusion:** We demonstrate that MAGeT-Brain produces consistent whole hippocampal segmentations using only 9 atlases, or fewer, with various hippocampal definitions, disease populations, and image acquisition types. Additionally, we show that MAGeT-Brain identifies hippocampal subfields in standard 3T T1-weighted images with overlap scores comparable to competing methods.
