# cersuit

Cerebellar segmentation with the [SUIT atlas and toolbox](https://www.diedrichsenlab.org/imaging/suit.htm). In the container, the pipeline is installed in the /opt/cersuit directory. Matlab code is in the src directory, and the entrypoint is src/cersuit.m. Compiled Matlab code for use in the singularity container without a Matlab license is in bin.

See the external directory for links, references, and license information for the underlying SPM12 and SUIT Matlab software. [FSL version 6.0.2](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki) is also used for image file manipulation and creating the QA PDF.

The container has a full installation of both SPM12 (compiled) and FSL. However, the SPM12 GUI will probably not run correctly due to some missing graphics libraries in the container OS.

## Requirements/Prerequisites

- cat12_ss2p0 pipeline

## Version Information

- Current Version: cersuit_v2.1.0
- Processor Name: cersuit_v2.1.0_processor.yaml
- Singularity Recipe and Code: https://github.com/baxpr/cersuit
- SHA256 Hash: cersuit_v2.1.0.sif (SHA256 34cf9101e557bf3a6a1dc1b93635b0bd68100d02882b8151b6775e6a84263010)

## Examples

[cersuit_v2.1.0](pdfs/cersuit_v2.1.0_301.pdf)

## Assumption and User Guide

**Inputs and Parameters**

- temporary-home-dir: Matlab will use this for temp files
- tmp-dir: Other location for temp files
- input-dir: Directory containing the input T1 image file
- output-dir: Outputs will be stored here
- t1-niigz-filename: Filename of the input T1 – expecting .nii.gz
- mask-threshold: SPM mask threshold for separating brain from background
- project-name: Project/subject/session/scan names from XNAT, if XNAT is used. These are only used to decorate the PDF report.
- subject-name
- session-name
- scan-name

**Outputs**

- PDF report for quality assurance
  - PDF: cersuit.pdf
- Transformation from native to atlas space
  - AFFINE: Affine_c_t1_seg1.mat
  - FLOWFIELD: u_a_c_t1_seg1.nii.gz
- Cropped T1 in both spaces
  - T1_CROP_NATIVE: c_t1.nii.gz
  - T1_CROP_SUIT: wc_t1.nii.gz
- Cerebellum mask, segmented gray matter and white matter volume fraction images in native and atlas space
  - MASK_NATIVE: c_t1_pcereb.nii.gz
  - GRAY_NATIVE: c_t1_seg1.nii.gz
  - WHITE_NATIVE: c_t1_seg2.nii.gz
  - MASK_SUIT: wc_t1_pcereb.nii.gz
  - GRAY_SUIT: wc_t1_seg1.nii.gz
  - WHITE_SUIT: wc_t1_seg2.nii.gz
- Jacobian-modulated gray and white matter images in atlas space
  - GRAYMOD_SUIT: wdc_t1_seg1.nii.gz
  - WHITEMOD_SUIT: wdc_t1_seg2.nii.gz
- Segmented regions in native and atlas space, with lookup table
  - SEG_NATIVE: iw_Lobules-SUIT_u_a_c_t1_seg1.nii.gz
  - SEG_SUIT: Lobules-SUIT.nii.gz
  - SEG_LUT: Lobules-SUIT-lut.txt
- Volumetry of segmented regions, computed from native space images. The “Total” is the volume of the atlas region after transformation to native space. The “Gray” is the sum of voxel gray matter fraction within the atlas region, in native space; similar for “White”.
  - SEG_NATIVE_VOLS: iw_Lobules-SUIT_u_a_c_t1_seg1-volumes.csv

**Usage**
```
singularity run --contain --cleanenv \
  --home  \
  --bind :/tmp \
  --bind :/INPUTS \
  --bind :/OUTPUTS \
  .simg \
  out_dir /OUTPUTS \
  t1_niigz /INPUTS/ \
  maskp  \
  project  \
  subject  \
  session  \
  scan 
 ```

## References

- [Diedrichsen, J. (2006). A spatially unbiased atlas template of the human cerebellum. Neuroimage, 33, 1, p. 127-138.](https://www.sciencedirect.com/science/article/abs/pii/S1053811906006410?via%3Dihub)
This article presents a new high-resolution atlas template of the human, cerebellum and brainstem, based on the anatomy of 20 young healthy individuals. The atlas is spatially unbiased, i.e., the location of each structure is equal to the expected location of that structure across individuals in MNI space, a result that is cross-validated with an independent sample of 16 individuals. At the same time, the new template preserves the anatomical detail of cerebellar structures through a nonlinear atlas generation algorithm. In comparison to current whole-brain templates, it allows for an improved voxel-by-voxel normalization for functional MRI and lesion analysis. Alignment to the template requires that the cerebellum and brainstem are isolated from the surrounding tissue, a process for which an automated algorithm has been developed. Compared to normalization to the MNI whole-brain template, the new method strongly improves the alignment of individual fissures, reducing their spatial spread by 60%, and improves the overlap of the deep cerebellar nuclei. Applied to functional MRI data, the new normalization technique leads to a 5–15% increase in peak t values and in the activated volume in the cerebellar cortex for movement vs. rest contrasts. This indicates that the new template significantly improves the overlap of functionally equivalent cerebellar regions across individuals. The template and software are freely available as an SPM-toolbox, which also allows users to relate the new template to the annotated volumetric (Schmahmann, J.D., Doyon, J., Toga, A., Petrides, M., Evans, A. (2000). MRI atlas of the human cerebellum. San Diego: Academic Press) and surface-based (Van Essen, D.C. (2002a) Surface-based atlases of cerebellar cortex in the human, macaque, and mouse. Ann. N. Y. Acad. Sci. 978:468–479.) atlas of one individual, the “colin27”-brain.

- [Diedrichsen, J., Balsters, J. H., Flavell, J., Cussans, E., & Ramnani, N. (2009). A probabilistic atlas of the human cerebellum. Neuroimage 46(1):39-46.](https://www.sciencedirect.com/science/article/abs/pii/S1053811909000809?via%3Dihub)
The functional organization of the [cerebellum](https://www.sciencedirect.com/topics/medicine-and-dentistry/cerebellum) is reflected in large part by the unique afferent and efferent connectivity of the individual cerebellar lobules. This functional diversity on a relatively small spatial scale makes accurate localization methods for human functional imaging and anatomical patient-based research indispensable. Here we present a probabilistic atlas of the cerebellar lobules in the anatomical space defined by the MNI152 template. We separately masked the lobules on T1-weighted MRI scans (1 mm isotropic resolution) of 20 healthy young participants (10 male, 10 female, average age 23.7 yrs). These cerebella were then aligned to the standard or non-linear version of the whole-brain MNI152 template using a number of commonly used normalization algorithms, or to a previously published cerebellum-only template (Diedrichsen, J., 2006. A spatially unbiased atlas template of the human cerebellum. NeuroImage 33, 127–138.). The resulting average overlap was higher for the cerebellum-only template than for any of the whole-brain normalization methods. The probabilistic maps allow for the valid assignment of functional activations to specific cerebellar lobules, while providing a quantitative measure of the uncertainty of such assignments. Furthermore, maximum probability maps derived from these atlases can be used to define regions of interest (ROIs) in [functional neuroimaging](https://www.sciencedirect.com/topics/medicine-and-dentistry/functional-neuroimaging) and neuroanatomical research. The atlas, made freely available online, is compatible with a number of widely used analysis packages.

- [Diedrichsen, J., Maderwald, S., Kuper, M., Thurling, M., Rabe, K., Gizewski, E. R., et al. (2011). Imaging the deep cerebellar nuclei: A probabilistic atlas and normalization procedure. Neuroimage 54(3):1786-94](https://www.sciencedirect.com/science/article/abs/pii/S1053811910013273?via%3Dihub)
The [deep cerebellar nuclei (DCN)](https://www.sciencedirect.com/topics/neuroscience/deep-cerebellar-nuclei) are a key element of the cortico-cerebellar loop. Because of their small size and functional diversity, it is difficult to study them using [magnetic resonance imaging (MRI)](https://www.sciencedirect.com/topics/medicine-and-dentistry/magnetic-resonance-imaging). To overcome these difficulties, we present here three related methodological advances. First, we used [susceptibility-weighted imaging (SWI)](https://www.sciencedirect.com/topics/neuroscience/susceptibility-weighted-imaging) at a high-field strength (7 T) to identify the [dentate, globose, emboliform and fastigial nucleus](https://www.sciencedirect.com/topics/neuroscience/dentate-nucleus) in 23 human participants. Due to their high iron content, the DCN are visible as hypo-intensities. Secondly, we generated probabilistic maps of the deep cerebellar nuclei in MNI space using a number of common normalization techniques. These maps can serve as a guide to the average location of the DCN, and are integrated into an existing probabilistic atlas of the human cerebellum (Diedrichsen et al., 2009). The maps also quantify the variability of the anatomical location of the deep cerebellar nuclei after normalization. Our results indicate that existing normalization techniques do not provide satisfactory overlap to analyze the functional specialization within the DCN. We therefore thirdly propose a ROI-driven normalization technique that utilizes both information from a T1-weighted image and the hypo-intensity from a T2*-weighted or SWI image to ensure overlap of the nuclei. These techniques will promote the study of the functional specialization of subregions of the DCN using MRI.

- [Diedrichsen, J. & Zotow, E. (2015). Surface-based display of volume-averaged cerebellar data. PLoS One, 7, e0133402.](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0133402)
The paper presents a flat representation of the human cerebellum, useful for visualizing functional imaging data after volume-based normalization and averaging across subjects. Instead of reconstructing individual cerebellar surfaces, the method uses a white- and grey-matter surface defined on volume-averaged anatomical data. Functional data can be projected along the lines of corresponding vertices on the two surfaces. The flat representation is optimized to yield a roughly proportional relationship between the surface area of the 2D-representation and the volume of the underlying cerebellar grey matter. The map allows users to visualize the activation state of the complete cerebellar grey matter in one concise view, equally revealing both the anterior-posterior (lobular) and medial-lateral organization. As examples, published data on resting-state networks and task-related activity are presented on the flatmap. The software and maps are freely available and compatible with most major neuroimaging packages.
