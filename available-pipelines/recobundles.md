# RecoBundles

RecoBundles is a white matter bundle recognition method developed by Garyfallidis et al [1]. It uses streamline registration and clustering to extract streamline bundles from the patient streamline space based on prior model bundles. In this implementation, preprocessed diffusion data are first converted to a tractogram. The fiber orientation distribution is calculated via constrained spherical deconvolution [2], which is then used to perform probabilistic fiber tracking. This tractogram is next registered to the model space [3], and the RecoBundles algorithm is applied to extract up to 78 streamline bundles. The Diffusion in Python (Dipy) software package was used to implement the RecoBundles algorithm and all tracking operations [4].

## Requirements/Prerequisites

- dtiQA/prequal pipeline

## Version Information

- Current Version: RecoBundles_v1.0.2
- Processor Name: RecoBundles_v1.0.2_processor.yaml
- Singularity Recipe and Code: https://github.com/MASILab/RecoBundles-spider
- SHA256 Hash: RecoBundles_v1.0.2.simg (SHA256 2461bf7cafe62002d3ef0d431e602bbcbec50b9886e66d28be900d0b16073882)

## Examples

- [RecoBundles_v1](recobundles_dti_T1W.pdf)
- [RecoBundles_v1](recobundles_dti2_T1W.pdf)
- [RecoBundles_v1](recobundles_dtiapa_T1W.pdf)
- [RecoBundles_v1](recobundles_LU_hardi_T1W.pdf)
- [RecoBundles_v1](recobundles_dti_T1.pdf)
- [RecoBundles_v1](recobundles_LU_dti2_T1.pdf)
- [RecoBundles_v1](recobundles_dtiapa_T1.pdf)
- [RecoBundles_v1](recobundles_LU_hardi_T1.pdf)

## Inputs

- dwmri.nii.gz (from dtiQA – PREPROCESSED)
- dwmri.bval (from dtiQA – PREPROCESSED)
- dwmri.bvec (from dtiQA – PREPROCESSED)
- mask.nii.gz (from dtiQA – PREPROCESSED)
- t1.nii.gz (used for visualizing tracks for QA)

## Parameters

- num_seeds: Number of seeds to use when generating streamlines [recommended: 1000000]
- trk_method: String specifying streamline tracking method; options are ‘probabilistic’ and ‘deterministic’
- project: String describing project (used to label PDF output)
- subject: String describing subject (used to label PDF output)
- session: String describing session (used to label PDF output)
- resources: String describing scans input above (used to label PDF output)

## Outputs

- PDF
  - recobundles_QA.pdf
- RECOBUNDLES
  - XXX.trk tractograms for all bundles found

## Input Assumptions

- T1 image is consistent with a conversion from a DICOM using dcm2niix by Chris Rorden and are raw NIFTIs without distortion correction.
- The location of b0 images inside dwmri do not matter.
- dwmri has been preprocessed using the dtiQA_v6 or dtiQA_v7 pipeline.

## Processing Pipeline

1. Extract the b0 image and highest shell (if more than on shell is present) from the dwmri image.
2. Fit tensor model for each voxel of dwmri image within the whole brain mask.
3. Estimate the fiber response function, which is then used to fit a constrained spherical deconvolution (CSD) model.
4. Track streamlines using chosen tracking method (trk_method), from the number of chosen seeds (num_seeds), and terminating tracking at a fractional anisotropy (FA) threshold of 0.2.
   - If using deterministic tracking, DIPY’s DeterministicMaximumDirectionGetter is used to drive streamline generation. It’s derived from the CSD model’s spherical harmonic coefficients, with a max angle of 25, PMF threshold of 0.1, and relative peak threshold of 0.5.
   - If using probabilistic tracking, DIPY’s DeterministicMaximumDirectionGetter is used to drive streamline generation. It’s derived from the CSD model’s spherical harmonic coefficients, with a max angle of 25, PMF threshold of 0.1, and relative peak threshold of 0.5.
5. Register the subject’s whole-brain tractogram to MNI streamline template.
6. Use DIPY’s RecoBundles algorithm to extract indices (in subject space) of each streamline bundle from the subject’s whole-brain tractogram that match with the model bundles.
7. Use indices from 7 to isolate recognized bundles in subject space.
8. Visualize the recognized bundles.
   - On the first page we describe the methods used for that run of the pipeline (what inputs were provided, what sort of preprocessing happened, etc.).
   - On the second page we show the whole-brain tractogram overlaid on the T1 volume for quality assurance.
   - On the third page we show which bundles were found and which ones failed.
   - The remaining pages contain visualizations of all recognized bundles. Each visualization shows a tri-planar view of the bundle overlaid on a transparent slice of the subject’s T1 for anatomical context.

## References

- [E. Garyfallidis et al., “Recognition of white matter bundles using local and global streamline-based registration and clustering,” Neuroimage, vol. 170, pp. 283–295, 2018.](https://www.sciencedirect.com/science/article/abs/pii/S1053811917305839)
Virtual dissection of diffusion MRI tractograms is cumbersome and needs extensive knowledge of white matter anatomy. This virtual dissection often requires several inclusion and exclusion regions-of-interest that make it a process that is very hard to reproduce across experts. Having automated tools that can extract white matter bundles for tract-based studies of large numbers of people is of great interest for neuroscience and neurosurgical planning. The purpose of our proposed method, named RecoBundles, is to segment white matter bundles and make virtual dissection easier to perform. This can help explore large tractograms from multiple persons directly in their native space. RecoBundles leverages latest state-of-the-art streamline-based registration and clustering to recognize and extract bundles using prior bundle models. RecoBundles uses bundle models as shape priors for detecting similar streamlines and bundles in tractograms. RecoBundles is 100% streamline-based, is efficient to work with millions of streamlines and, most importantly, is robust and adaptive to incomplete data and bundles with missing components. It is also robust to pathological brains with tumors and deformations. We evaluated our results using multiple bundles and showed that RecoBundles is in good agreement with the neuroanatomical experts and generally produced more dense bundles. Across all the different experiments reported in this paper, RecoBundles was able to identify the core parts of the bundles, independently from tractography type (deterministic or probabilistic) or size. Thus, RecoBundles can be a valuable method for exploring tractograms and facilitating tractometry studies.

- [M. Descoteaux, R. Deriche, T. R. Knösche, and A. Anwander, “Deterministic and probabilistic tractography based on complex fibre orientation distributions,” IEEE Trans. Med. Imaging, vol. 28, no. 2, pp. 269–286, 2009.](https://pubmed.ncbi.nlm.nih.gov/19188114/)
We propose an integral concept for tractography to describe crossing and splitting fibre bundles based on the fibre orientation distribution function (ODF) estimated from high angular resolution diffusion imaging (HARDI). We show that in order to perform accurate probabilistic tractography, one needs to use a fibre ODF estimation and not the diffusion ODF. We use a new fibre ODF estimation obtained from a sharpening deconvolution transform (SDT) of the diffusion ODF reconstructed from q-ball imaging (QBI). This SDT provides new insight into the relationship between the HARDI signal, the diffusion ODF, and the fibre ODF. We demonstrate that the SDT agrees with classical spherical deconvolution and improves the angular resolution of QBI. Another important contribution of this paper is the development of new deterministic and new probabilistic tractography algorithms using the full multidirectional information obtained through use of the fibre ODF. An extensive comparison study is performed on human brain datasets comparing our new deterministic and probabilistic tracking algorithms in complex fibre crossing regions. Finally, as an application of our new probabilistic tracking, we quantify the reconstruction of transcallosal fibres intersecting with the corona radiata and the superior longitudinal fasciculus in a group of eight subjects. Most current diffusion tensor imaging (DTI)-based methods neglect these fibres, which might lead to incorrect interpretations of brain functions.

- [E. Garyfallidis, O. Ocegueda, D. Wassermann, and M. Descoteaux, “Robust and efficient linear registration of white-matter fascicles in the space of streamlines,” Neuroimage, vol. 117, pp. 124–140, 2015.](https://www.sciencedirect.com/science/article/abs/pii/S1053811915003961)
The neuroscientific community today is very much interested in analyzing specific white matter bundles like the arcuate fasciculus, the corticospinal tract, or the recently discovered Aslant tract to study sex differences, lateralization and many other connectivity applications. For this reason, experts spend time manually segmenting these fascicles and bundles using streamlines obtained from diffusion MRI tractography. However, to date, there are very few computational tools available to register these fascicles directly so that they can be analyzed and their differences quantified across populations. In this paper, we introduce a novel, robust and efficient framework to align bundles of streamlines directly in the space of streamlines. We call this framework Streamline-based Linear Registration. We first show that this method can be used successfully to align individual bundles as well as whole brain streamlines. Additionally, if used as a piecewise linear registration across many bundles, we show that our novel method systematically provides higher overlap (Jaccard indices) than state-of-the-art nonlinear image-based registration in the white matter. We also show how our novel method can be used to create bundle-specific atlases in a straightforward manner and we give an example of a probabilistic atlas construction of the optic radiation. In summary, Streamline-based Linear Registration provides a solid registration framework for creating new methods to study the white matter and perform group-level tractometry analysis.

- [E. Garyfallidis et al., “Dipy, a library for the analysis of diffusion MRI data,” Front. Neuroinform., vol. 8, no. FEB, pp. 1–17, 2014.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3931231/)
Diffusion Imaging in Python (Dipy) is a free and open source software project for the analysis of data from diffusion magnetic resonance imaging (dMRI) experiments. dMRI is an application of MRI that can be used to measure structural features of brain white matter. Many methods have been developed to use dMRI data to model the local configuration of white matter nerve fiber bundles and infer the trajectory of bundles connecting different parts of the brain. Dipy gathers implementations of many different methods in dMRI, including: diffusion signal pre-processing; reconstruction of diffusion distributions in individual voxels; fiber tractography and fiber track post-processing, analysis and visualization. Dipy aims to provide transparent implementations for all the different steps of dMRI analysis with a uniform programming interface. We have implemented classical signal reconstruction techniques, such as the diffusion tensor model and deterministic fiber tractography. In addition, cutting edge novel reconstruction techniques are implemented, such as constrained spherical deconvolution and diffusion spectrum imaging (DSI) with deconvolution, as well as methods for probabilistic tracking and original methods for tractography clustering. Many additional utility functions are provided to calculate various statistics, informative visualizations, as well as file-handling routines to assist in the development and use of novel techniques. In contrast to many other scientific software projects, Dipy is not being developed by a single research group. Rather, it is an open project that encourages contributions from any scientist/developer through GitHub and open discussions on the project mailing list. Consequently, Dipy today has an international team of contributors, spanning seven different academic institutions in five countries and three continents, which is still growing.
