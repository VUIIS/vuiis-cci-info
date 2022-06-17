# Pipeline Name

Long Version Of Pipeline Name If Needed

Overview/description of pipeline is a paragraph or two here.

**Inputs**

- T1 image in NIFTI format
- T2 image in NIFTI format
- Output XYZ of [prerequisite pipeline 1](prereq-pipeline1.md)
- ...

**Version**

- Current Version: v1.3.4
- Processor: pipeline_v1.3.4.yaml
- Singularity Image: pipeline_v1.3.4.simg (SHA256 <SHA256-hash-of-the-container-file>)

**Release Notes**

- v1.3.4 (2022-06-16)
  - Release notes here if available

- v1.3.3 (2022-01-01)
  - Historical release notes if available

## Examples (QA PDFs)

- [Example 1](pdfs/example1.pdf)


## Code

- Repository 1: https://github.com/whatever1
- Repository 2: https://github.com/whatever2


## References

- [Harrigan RL, Yvernault BC, Boyd BD, Damon SM, Gibney KD, Conrad BN, Phillips NS, Rogers BP, Gao Y, Landman BA. Vanderbilt University Institute of Imaging Science Center for Computational Imaging XNAT: A multimodal data archive and processing environment. Neuroimage. 2016 Jan 1;124(Pt B):1097-1101. doi: 10.1016/j.neuroimage.2015.05.021. Epub 2015 May 16. PMID: 25988229; PMCID: PMC4646735.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4646735/) The Vanderbilt University Institute for Imaging Science (VUIIS) Center for Computational Imaging (CCI) has developed a database built on XNAT housing over a quarter of a million scans. The database provides framework for (1) rapid prototyping, (2) large scale batch processing of images and (3) scalable project management. The system uses the web-based interfaces of XNAT and RedCAP to allow for graphical interaction. A python middleware layer, the Distributed Automation for XNAT (DAX) package, distributes computation across the Vanderbilt Advanced Computing Center for Research and Education high performance computing center. All software are made available in open source for use in combining portable batch scripting (PBS) grids and XNAT servers.
