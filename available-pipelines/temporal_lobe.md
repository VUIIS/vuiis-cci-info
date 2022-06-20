# Temporal_Lobe

## Requirements/Prerequisites

- Multi_Atlas pipeline

## Version Information

- Current Version: Temporal_Lobe_v4.0.0
- Processor Name: Temporal_Lobe_v4.0.0_processor.yaml
- Singularity Recipe and Code: https://github.com/VUIIS/Temporal_Lobe_app
- SHA256 Hash: Temporal_Lobe_v4.0.0.simg (SHA256 e62e3ef66692493a3575c265dca4900b2eca4e14c086abac8b0bcda1d650a62b)

## References

- [Plassard AJ, McHugo M, Heckers S, Landman BA. Multi-Scale Hippocampal Parcellation Improves Atlas-Based Segmentation Accuracy. Proc SPIE Int Soc Opt Eng. 2017 Feb 11;10133:101332D. doi: 10.1117/12.2254425. Epub 2017 Feb 24. PMID: 28781411; PMCID: PMC5544133.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5544133/)
Known for its distinct role in memory, the hippocampus is one of the most studied regions of the brain. Recent advances in magnetic resonance imaging have allowed for high-contrast, reproducible imaging of the hippocampus. Typically, a trained rater takes 45 minutes to manually trace the hippocampus and delineate the anterior from the posterior segment at millimeter resolution. As a result, there has been a significant desire for automated and robust segmentation of the hippocampus. In this work we use a population of 195 atlases based on T1-weighted MR images with the left and right hippocampus delineated into the head and body. We initialize the multi-atlas segmentation to a region directly around each lateralized hippocampus to both speed up and improve the accuracy of registration. This initialization allows for incorporation of nearly 200 atlases, an accomplishment which would typically involve hundreds of hours of computation per target image. The proposed segmentation results in a Dice similiarity coefficient over 0.9 for the full hippocampus. This result outperforms a multi-atlas segmentation using the BrainCOLOR atlases (Dice 0.85) and FreeSurfer (Dice 0.75). Furthermore, the head and body delineation resulted in a Dice coefficient over 0.87 for both structures. The head and body volume measurements also show high reproducibility on the Kirby 21 reproducibility population (R2 greater than 0.95, p < 0.05 for all structures). This work signifies the first result in an ongoing work to develop a robust tool for measurement of the hippocampus and other temporal lobe structures.
