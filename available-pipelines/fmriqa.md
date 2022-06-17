# FMRIQA

## Requirements/Prerequisites

- Multi_Atlas pipeline

**or**

- Slant pipeline

## Version Information

- Current Version: fmriqa_v4.2.0
- Processor Name: fmriqa_v4.2.0_processor.yaml
- Singularity Recipe and Code: https://github.com/baxpr/fmriqa
- Container Location: shub://baxpr/fmriqa:v4.2.0
- SHA256 Hash: baxpr-fmriqa-master-v4.2.0.simg (SHA256 a9face3437fc0a0ea59881265a90f7463d22b57a3525cd54ca20582c92e5ed70)

## Examples

**VUIIS_ABCD**

- [fmriqa_v4](pdfs/fmriqa_ABCD_rsEPI_MB6R1_FSA.pdf)

**LANDMAN_UPGRAD**

- A: [fmriqa_v4](pdfs/fmriqa_v4_T1W_LU.pdf)

- B: [fmriqa_v4](pdfs/fmriqa_v4_T1_LU.pdf)

## Code

- [GitHub Repository for Current Spider](https://github.com/baxpr/fmriqa)

## References

- [Power JD, Barnes KA, Snyder AZ, Schlaggar BL, Petersen SE. Spurious but systematic correlations in functional connectivity MRI networks arise from subject motion [published correction appears in Neuroimage. 2012 Nov 1;63(2):999]. Neuroimage. 2012;59(3):2142–2154. doi:10.1016/j.neuroimage.2011.10.018](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0061737)
Here, we demonstrate that subject motion produces substantial changes in the timecourses of resting state functional connectivity MRI (rs-fcMRI) data despite compensatory spatial registration and regression of motion estimates from the data. These changes cause systematic but spurious correlation structures throughout the brain. Specifically, many long-distance correlations are decreased by subject motion, whereas many short-distance correlations are increased. These changes in rs-fcMRI correlations do not arise from, nor are they adequately countered by, some common functional connectivity processing steps. Two indices of data quality are proposed, and a simple method to reduce motion-related effects in rs-fcMRI analyses is demonstrated that should be flexibly implementable across a variety of software platforms. We demonstrate how application of this technique impacts our own data, modifying previous conclusions about brain development. These results suggest the need for greater care in dealing with subject motion, and the need to critically revisit previous rs-fcMRI work that may not have adequately controlled for effects of transient subject movements.

- [Power JD. A simple but useful way to assess fMRI scan qualities. Neuroimage. 2017;154:150–158. doi:10.1016/j.neuroimage.2016.08.009](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5296400/)
This short “how to” article describes a plot I find useful for assessing fMRI data quality. I discuss the reasoning behind the plot and how it is constructed. I create the plot in scans from several publicly available datasets to illustrate different kinds of fMRI signal variance, ranging from thermal noise to motion artifacts to respiratory-related signals. I also show how the plot can be used to understand the variance removed during denoising. Code to make the plot is provided with the article, and supplemental movies show plots for hundreds of additional subjects.
