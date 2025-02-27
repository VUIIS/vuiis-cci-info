# Available Pipelines

## Building Spiders 101

[Documentation for Creating Spiders](building_spiders.md)

## Preparing Matlab Code for Spider Conversion

[Requirements for Converting Matlab code-base to Spider](matlab_code_spider_conversion.md)

## Currently Available Pipelines

### Structural Segmentation / Template Registration

- [acapulco](acapulco.md) - ACAPULCO - Automatic Cerebellum Anatomical Parcellation Using U-Net with Locally Constrained Optimization ?????
- ASHS - ?????
- assemblynet - ?????
- BFC - ?????
- [BISCUIT, curve_extract, and surf_*](BISCUIT-curve_extract-surf.md) - Brain Shape Computing Toolbox – An Automated Pipeline for Cortical Morphometry
- [BrainAgeGap](brainagegap.md)
- [cat12_ss2p0](cat12_ss2p0.md) - Computational Anatomy Toolbox for SPM
- [cerebellum](cerebellum.md) - This singularity image does N4 bias field correction; MNI registration; Cerebellum parcellation; Report generation
- [cersuit](cersuit.md) - Cerebellar segmentation with the SUIT atlas and toolbox
- DnSeg - ?????
- [freesurfer](freesurfer.md) - Runs Freesurfer’s recon-all, plus hippocampus, thalamus, brainstem segmentation modules
- [FS6](fs6.md) - UPDATE TO FS7 ?????
- [LST](lst.md)
- [MaCRUISE](macruise.md) – Consistent cortical reconstruction and multi-atlas brain segmentation
- [magm_normalize](magm_normalize.md) – Computes a gray matter image from MultiAtlas output, and warps it to MNI space
- mri-reface - ?????
- [mriqc](mriqc.md) – Extracts Image Quality Metrics (IQMs) for anatomical and fMRI scans.
- [Multi_Atlas](multi_atlas.md) – loads the multi-atlas segmentation result images (SEG/orig_target_seg.nii.gz, and TICV/orig_target_ticv.nii.gz if available) and computes regional volumes
- [reface](reface.md)
- roi-resample - uses cat12 transform to resample an ROI image from atlas to participant native space.
- RWML - ?????
- [Slant](slant.md) - Deep Whole Brain High Resolution Segmentation
- [Temporal_Lobe](temporal_lobe.md)
- [thomas](thomas.md)

### Functional MRI

- [connprep](connprep.md) - Produces preprocessed fMRI images ready for connectivity analysis
- EDATQA - ?????
- [FMRIQA](fmriqa.md) - Motion realignment and creation of mean fMRI; Coregister T1 to mean fMRI; Compute SNR and quality metrics; Carpet plots, graphical report
- fmriprep - ?????
- [mriqc](mriqc.md) – Extracts Image Quality Metrics (IQMs) for anatomical and fMRI scans.
- [XCP](xcp.md) - Uses outputs of fMRIprep to generate denoised BOLD images, parcellated time series, functional connectivity matrices, and quality assessment reports.

### Diffusion

- [bedpostx](bedpostx.md) - FSL fiber orientation estimation for diffusion images
- [DTIQA/PreQual](dtiqa-prequal.md)- Preprocessing and quality checks for diffusion data
- [nobis_tracts](nobis_tracts.md) – Generate extended-amygdalar to brainstem structural connectomes from diffusion weighted and T1-weighted images
- [RecoBundles](recobundles.md)
- tbss-enigma - ?????

#### Preprocessing

#### Tractography

- [Connectivity Atlases Flow](connectivity-atlases-flow.md)
- [connectoflow](connectoflow.md)
- [rbx_flow](rbx_flow.md)
- [tractoflow](tractoflow.md)
- [tractometry_flow](tractometry_flow.md)
- [tracula](tracula.md)

#### NODDI/ODF Modeling

#### Misc

- AMYVIDQA - ?????
- EEG-EGI - ?????
- [examcard-to-txt](examcard-to-txt.md) - Convert examcards from DICOM to TXT, HTML, and PDF formats
- FEOBVQA - ?????
- mp2rage - ?????
- NMQA - ?????
- OCTQA_retina - ?????
- ON_MR_segmentation - ?????
- ON_MR_sheath_segmentation - ?????
- petreg-CTAC - ?????
- pibqa - ?????
- [RSFC_CONN](rsfc_conn.md)
- SAMSEG - ?????
- synbold - ?????
