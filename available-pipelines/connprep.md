# XCP-D

- [Documentation](https://xcp-d.readthedocs.io/en/latest/)
- [Extras Repo](https://github.com/VUIIS/xcpd-processors/)

## Requirements/Prerequisites

- fMRIprep

## Version Information

- Current Version: XCP_v0.1.0
- Processor Name: xcp_v0.1.0.yaml
- Singularity Recipe and Code: [Github](https://github.com/PennLINC/xcp_d)
- SHA256 Hash: XCP_v0.1.0 (SHA256 db040bebc3b5a970bd73b8957d0c3398b9711111e63a91028f835475bc6c0148  XCP_v0.1.0.simg)

## Examples

- XCP BOLD report: [xcp_v0](pdfs/xcp_example.pdf)

# connprep (DEPRECATED)

The connprep spider produces preprocessed fMRI images ready for connectivity analysis.

## Requirements/Prerequisites

- cat12_ss2p0 pipeline

## Version Information

- THIS VERSION IS DEPRECATED. SEE ABOVE FOR NEW VERSION
- Current Version: connprep_v2.1.0
- Processor Name: connprep_v2.1.0_processor.yaml
- Singularity Recipe and Code: https://github.com/baxpr/connprep/tree/v2.1.0
- Container Location: shub://baxpr/connprep:v2.1.0
- SHA256 Hash: baxpr-connprep-master-v2.1.0.simg (SHA256 7b435149d87beccf7fe15322f5a832b456dbe7971eb74cd3bf7c4357130822f4)

## Examples

**VUIIS_ABCD**

- [connprep_v2](pdfs/connprep_601-1.pdf)

**LANDMAN_UPGRAD**

- A: [connprep_v2](pdfs/connprep_v2_T1W_RESTING.pdf)
- B: [connprep_v2](pdfs/connprep_v2_T1_RESTING.pdf)

## Code

[GitHub Repo for Current Spider](https://github.com/baxpr/connprep)
