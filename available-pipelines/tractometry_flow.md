# tractometry_flow 


This pipeline allows you to extract tractometry information by combining subjects’ WM bundles and diffusion MRI metrics. There is two way the tractometry informatin is computed:

Average metric inside of a WM bundle volume (voxels occupied by at least one streamline)
Average metric inside of a subsection of WM bundle volume (voxels occupied by at least one streamline)
The second method ‘cut’ the bundle in section so variation can be observed along the length. The exact steps are described in [1]. This approach is similar to what is presented in [1,2]. All reported metrics are weighted by streamline density, this way the values of the core/center of bundles are more represented than spurious streamlines and outliers.

Bundle_Metrics_Stats_In_Endpoints/ contains maps for each bundle where the average value along a streamlines are projected to the last points for cortical projection visualisation or statistics.

To fully QA the data, we recommand to download the labels map TRK file and inspect them in MI-Brain (https://www.imeka.ca/mi-brain/). The pipeline was optimized for bundles with large spatial extend (probabilistic tractography) extracted with RecobundlesX using this atlas: https://zenodo.org/record/4630660#.

## Requirements/Prerequisites

- rbx_flow pipeline
- tractoflow pipeline

## Version Information

- Current Version: tractometry_flow_v1.0.0
- Processor Name: tractometry_flow_v1.0.0_processor.yaml
- Singularity Recipe and Code: https://github.com/MASILab/tractometry_flow_spider
- SHA256 Hash: tractometry_flow_v1.0.0.simg (SHA256 c9cd46ee578e442825ef92b3bc4d7e91f84d345b74969ec816b65a5032199547)

## Input Assumptions and Parameters Choice 

Tractogram reconstruction was adequate (millions of streamlines, no lesions unless corrected accordingly) Bundle segmentation was adaquate (each bundle is dense, without obvious ‘defect’) The parameters ‘nb_pts’ is between 2-100 This pipeline does not perform any statistical analysis, this should be planned separately beforehand

## Inputs

- bundles/*.trk (from RBX Flow)
- centroids/*.trk (from RBX Flow)
- fa.nii.gz (from Tractoflow)
- md.nii.gz (from Tractoflow)
- rd.nii.gz (from Tractoflow)
- ad.nii.gz (from Tractoflow)
- nufo.nii.gz (from Tractoflow)
- afd_total.nii.gz (from Tractoflow)
- afd_sum.nii.gz (from Tractoflow)
- afd_max.nii.gz (from Tractoflow)

## Outputs

**Reporting**

- report.html
- report.pdf

**Bundles Statistics**

- stats_xlsx/
- stats_json/

**Bundle Maps**

- labels_maps/
- bundle_endpoints_metrics/

## References

- [Cousineau, Martin, et al. “A test-retest study on Parkinson’s PPMI dataset yields statistically significant white matter fascicles. “NeuroImage: Clinical 16, 222-233 (2017) doi:10.1016/j.nicl.2017.07.020](https://pubmed.ncbi.nlm.nih.gov/28794981/)
In this work, we propose a diffusion MRI protocol for mining Parkinson’s disease diffusion MRI datasets and recover robust disease-specific biomarkers. Using advanced high angular resolution diffusion imaging (HARDI) crossing fiber modeling and tractography robust to partial volume effects, we automatically dissected 50 white matter (WM) fascicles. These fascicles connect deep nuclei (thalamus, putamen, pallidum) to different cortical functional areas (associative, motor, sensorimotor, limbic), basal forebrain and substantia nigra. Then, among these 50 candidate WM fascicles, only the ones that passed a test-retest reproducibility procedure qualified for further tractometry analysis. Leveraging the unique 2-timepoints test-retest Parkinson’s Progression Markers Initiative (PPMI) dataset of over 600 subjects, we found statistically significant differences in tract profiles along the subcortico-cortical pathways between Parkinson’s disease patients and healthy controls. In particular, significant increases in FA, apparent fiber density, tract-density and generalized FA were detected in some locations of the nigro-subthalamo-putaminal-thalamo-cortical pathway. This connection is one of the major motor circuits balancing the coordination of motor output. Detailed and quantifiable knowledge on WM fascicles in these areas is thus essential to improve the quality and outcome of Deep Brain Stimulation, and to target new WM locations for investigation.

- [Yeatman, Jason D., et al. “Tract profiles of white matter properties: automating fiber-tract quantification.” PloS one 7.11 (2012): e49790.](https://pubmed.ncbi.nlm.nih.gov/23166771/)
Tractography based on diffusion weighted imaging (DWI) data is a method for identifying the major white matter fascicles (tracts) in the living human brain. The health of these tracts is an important factor underlying many cognitive and neurological disorders. In vivo, tissue properties may vary systematically along each tract for several reasons: different populations of axons enter and exit the tract, and disease can strike at local positions within the tract. Hence quantifying and understanding diffusion measures along each fiber tract (Tract Profile) may reveal new insights into white matter development, function, and disease that are not obvious from mean measures of that tract. We demonstrate several novel findings related to Tract Profiles in the brains of typically developing children and children at risk for white matter injury secondary to preterm birth. First, fractional anisotropy (FA) values vary substantially within a tract but the Tract FA Profile is consistent across subjects. Thus, Tract Profiles contain far more information than mean diffusion measures. Second, developmental changes in FA occur at specific positions within the Tract Profile, rather than along the entire tract. Third, Tract Profiles can be used to compare white matter properties of individual patients to standardized Tract Profiles of a healthy population to elucidate unique features of that patient’s clinical condition. Fourth, Tract Profiles can be used to evaluate the association between white matter properties and behavioral outcomes. Specifically, in the preterm group reading ability is positively correlated with FA measured at specific locations on the left arcuate and left superior longitudinal fasciculus and the magnitude of the correlation varies significantly along the Tract Profiles. We introduce open source software for automated fiber-tract quantification (AFQ) that measures Tract Profiles of MRI parameters for 18 white matter tracts. With further validation, AFQ Tract Profiles have potential for informing clinical management and decision-making.

- [Chandio, Bramsh Qamar, et al. “Bundle analytics, a computational framework for investigating the shapes and profiles of brain pathways across populations.” Scientific reports 10.1 (2020): 1-18.](https://pubmed.ncbi.nlm.nih.gov/33051471/)
Tractography has created new horizons for researchers to study brain connectivity in vivo. However, tractography is an advanced and challenging method that has not been used so far for medical data analysis at a large scale in comparison to other traditional brain imaging methods. This work allows tractography to be used for large scale and high-quality medical analytics. BUndle ANalytics (BUAN) is a fast, robust, and flexible computational framework for real-world tractometric studies. BUAN combines tractography and anatomical information to analyze the challenging datasets and identifies significant group differences in specific locations of the white matter bundles. Additionally, BUAN takes the shape of the bundles into consideration for the analysis. BUAN compares the shapes of the bundles using a metric called bundle adjacency which calculates shape similarity between two given bundles. BUAN builds networks of bundle shape similarities that can be paramount for automating quality control. BUAN is freely available in DIPY. Results are presented using publicly available Parkinson’s Progression Markers Initiative data.
