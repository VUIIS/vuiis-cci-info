# DTIQA/Prequal

PreQual (dtiQA v7 Multi) was developed at Vanderbilt under the project name “dtiQA v7 Multi”. PreQual v1.0.0 represents dtiQA v7.2.0. Thus, on XNAT, dtiQA v7.2.x refers to PreQual v1.0.x. 

## Version Information

- Current Version: We are currently recommending prequal_v1.0.6 assessors
- Examples
  - prequal-1j-synb0: One diffusion scan, j phase encoding direction, synb0
  - prequal-2j-rpe: Two diffusion scans with opposite phase encoding on j, regular topup
  - prequal-3j-synb0: Three diffusion scans all the same phase encoding, synb0

## Examples

- [dtiQA_v7](pdfs/dtiQA_v7_T1W_DTIAPA_HARDI.pdf)

## Code

[PreQual Git Repository](https://github.com/MASILab/PreQual)

## References

- [Lauzon CB, Asman AJ, Esparza ML, Burns SS, Fan Q, Gao Y, et al. (2013) Simultaneous Analysis and Quality Assurance for Diffusion Tensor Imaging. PLoS ONE 8(4): e61737. https://doi.org/10.1371/journal.pone.0061737](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3254728/)
Diffusion tensor imaging (DTI) enables non-invasive, cyto-architectural mapping of in vivo tissue microarchitecture through voxel-wise mathematical modeling of multiple magnetic resonance imaging (MRI) acquisitions, each differently sensitized to water diffusion. DTI computations are fundamentally estimation processes and are sensitive to noise and artifacts. Despite widespread adoption in the neuroimaging community, maintaining consistent DTI data quality remains challenging given the propensity for patient motion, artifacts associated with fast imaging techniques, and the possibility of hardware changes/failures. Furthermore, the quantity of data acquired per voxel, the non-linear estimation process, and numerous potential use cases complicate traditional visual data inspection approaches. Currently, quality inspection of DTI data has relied on visual inspection and individual processing in DTI analysis software programs (e.g. DTIPrep, DTI-studio). However, recent advances in applied statistical methods have yielded several different metrics to assess noise level, artifact propensity, quality of tensor fit, variance of estimated measures, and bias in estimated measures. To date, these metrics have been largely studied in isolation. Herein, we select complementary metrics for integration into an automatic DTI analysis and quality assurance pipeline. The pipeline completes in 24 hours, stores statistical outputs, and produces a graphical summary quality analysis (QA) report. We assess the utility of this streamlined approach for empirical quality assessment on 608 DTI datasets from pediatric neuroimaging studies. The efficiency and accuracy of quality analysis using the proposed pipeline is compared with quality analysis based on visual inspection. The unified pipeline is found to save a statistically significant amount of time (over 70%) while improving the consistency of QA between a DTI expert and a pool of research associates. Projection of QA metrics to a low dimensional manifold reveal qualitative, but clear, QA-study associations and suggest that automated outlier/anomaly detection would be feasible.
