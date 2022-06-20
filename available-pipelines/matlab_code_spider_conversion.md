# Preparing Matlab Code for Spider Conversion

### Requirements for converting Matlab code-base to spider.

When submitting MATLAB code to the CCI for spider-conversion, please ensure that the code meets the following guidelines:

- All input files should be found in a specific directory (in_dir) and should be provided as an input parameter/command line option with a fully specified path.
- All output files should be stored in specific directory (out_dir). Output directory should also be provided as an input parameter/command line option.
- Provide a list of all required inputs and expected outputs.
- Provide a list of required Matlab packages for the code-base.
- All functions should be written to operate on a single session, not loop through multiple.
- Additional parameters must be passed in as command line options.
- Any information you would like added to the output PDF should be saved within the Matlab function in the appropriate format (e.g. figures as PNG, tables/statistics as CSV).
- Use the ouput directory for temporary working space. Do not have a separate work_dir for intermediate processing, as this will lead to errors.
- All code should be stored in a Github repository.

## Additional Notes

- DO NOT use nifti toolbox functions (load_nii, load_untouch_nii, save_nii, etc.). These functions are out of date and often result in errors or missing information. Instead, use the SPM12 nifti functions (see this [Github repository](https://github.com/VUIIS/spm_readwrite_nii) for example).
- Input filenames may be assumed/hardcoded into the script. For example, T1 files from XNAT will always be named /path/to/T1.nii.gz.
- For MATLAB, any usage of the ‘addpath’ function must be skipped if running a compiled version.
- If any files will be included in the container, use which function to load, e.g. load(which(‘example.mat’)). If any input parameters will vary, pass them into the function through the command line.
- DO NOT hardcode image parameters such as TR/TE. Any necessary parameters should either be extracted from the nifti file or passed as input parameters/optional arguments.
- Failure to specify in full where files are written will result in errors.
- Do not use ‘parfor’ or any functions from the Parallel computing toolbox, as these will not work in compiled Matlab code.

## Examples of Matlab code-base Containers

- https://github.com/VUIIS/hello-world-MCR
- https://github.com/VUIIS/demo-singularity-spm-freeview
- https://github.com/VUIIS/demo-singularity-matlab-fsl
