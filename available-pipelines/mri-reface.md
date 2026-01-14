# mri-reface

## Version Information

- Current Version: mri-reface_v0.3.3
- Processor Name: mri-reface_v0.3.3.yaml
- Container Location: [shub://baxpr/connprep:v2.1.0](https://www.nitrc.org/projects/mri_reface/)
- SHA256 Hash: mri-reface_v0.3.3.sif (SHA256 45a375f8f93762a5736f67f477a751d2fcf3f73ae0e1565d2a698d7f1b0ba3c2)

## References

- https://www.nitrc.org/projects/mri_reface/
- https://www.sciencedirect.com/science/article/pii/S1053811921001221
- https://www.sciencedirect.com/science/article/pii/S1053811922004761

## Notes

In local experience, mri_reface works more reliably on more cases and handles a greater variety of contrasts than other available deface/reface pipelines.

Here are the relevant outputs for our XNAT version:
- REFACE: nifti image that is the T1, but refaced
- FACEMASK: nifti image of the masked 'face' region
- QC: couple of PNG images with potentially useful views
- PDF: basically useless

It's meant to replace the participant face completely with a blurry generic face, not just try to blur out the existing face.
