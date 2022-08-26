# VUIIS CCI Facilities and Equipment Description

## Center for Computational Imaging

The Vanderbilt University Institute of Image Science (VUIIS) operates the Center for Computational Imaging (CCI) within the Human Imaging CORE (HIC). The mission of the CCI is to support collaborative image processing research at Vanderbilt by (1) creating infrastructure to interface medical image processing with high performance computing, (2) supporting implementation and standardization of medical image processing, and (3) facilitating collaboration on medical image processing. The CCI’s primary focus is on studies conducted at VUIIS, but the CCI actively support VUIIS participation in multi-university studies. The CCI has been directed by Baxter P. Rogers, Ph.D. since 2021.

To support image processing, the CCI operates (1) a research only PACS for VUIIS human imaging scanners (3T MRI, 7T MRI), (2) the xnat.vanderbilt.edu instance of XNAT running on a custom HyperV virtualization cluster with direct access to the ACCRE high performance computing facility, and (3) the Distributed Automation for XNAT (DAX) services that automate distribution of computation from xnat.vanderbilt.edu to the ACCRE compute grid. As of August 2022, VUIIS XNAT contains 556 projects, with 144527 imaging sessions from 88697 participants.

To support implementation and standardization, the CCI administers open-source repositories for medical image processing routines using the NIH supported Neuroimaging Informatics Tools and Resources Clearinghouse (NITRC) infrastructure. The pipeline modules (called assessors or spiders) capture all necessary provenance so that image processing routines can be reproducibly executed across projects. All spiders can be executed within DAX using the ACCRE grid, on private/secure grids, or in standalone fashion on workstations/laptops. A wide variety are available, including image segmentation, fMRI and diffusion preprocessing, and image defacing for anonymization.

To support collaboration, the CCI operates weekly problem solving work-sessions / face-to-face hack-a-thons. All community members are welcome to the open meetings during which concerns are raised, issues are identified, and potential solutions are addressed. The CCI uses Trello for graphical project management, bug reporting, task monitoring, and user follow-up. Additionally, the CCI runs an e-mail mailing list and online collaboration community forum. The core CCI team of collaborators consists of approximately two dozen staff engineers, post docs, and graduate students / research associates and supports all neuroimaging researchers across VUMC and VU who use Human Imaging Core services.

Bennett Landman, Ph.D. (the initiator and first Director of the CCI) and the CCI have a track record of community building around medical image processing. He developed and his group supports the Java Image Science Toolkit (JIST, open source on NITRC: https://www.nitrc.org/projects/jist/), which has been downloaded 15,490 times since 2009. Additionally, he has released and supported widely used MRI data resources at both 3T and 7T (Multi-Modal MRI Reproducibility Resource, on NITRC: https://www.nitrc.org/projects/multimodal/), which has been downloaded 25,077 times since 2009. More recently, the CCI group has released the DAX system for integrating REDCap, XNAT, and high performance computing (open source on GIT: https://github.com/VUIIS/dax).


## VUIIS CCI at ACCRE

The CCI maintains a close connection with the [Advanced Computing Center for Research and Education (ACCRE)](https://www.vanderbilt.edu/accre/). The CCI maintains three custom gateways on the ACCRE cluster:

- poplar.accre.vanderbilt.edu – 24 cores; 64 gigs of ram
- ginko.accre.vanderbilt.edu – 64 cores; 258 gigs of ram
- hickory.accre.vanderbilt.edu – 56 cores; 258 gigs of ram

The CCI has the following accre compute quota:

- Max 768 cpus; Max 5280 gigs of ram
- 16 GPU nodes

Additionally, we maintain a close relationship with the MASI lab which has the following accre compute quota:

- Max 528 cpus; Max 5280 gigs of ram

For access to these resources, please sign up for an ACCRE account [1] and contact the CCI staff at masi-admin@list.vanderbilt.edu.

## Related VU/VUMC Resources

1. ACCRE: http://www.accre.vanderbilt.edu
