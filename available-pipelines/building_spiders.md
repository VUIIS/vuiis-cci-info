# Building Spiders 101

A guide for transforming normal programs into singularity containers that can run on XNAT. An initial question that provides an overview of the spider ecosystem:

### What is the relationship between XNAT, DAX, slurm, the yaml file, ACCRE, and the singularity container?

- XNAT is the informatics platform where we want our scans and the results of our pipelines to be stored. We either manually upload scans to XNAT or XNAT receives data from PACS.
- DAX is the automation tool which checks on XNAT and determines the scan-pipelines combination that need to run and makes use of the yaml file and the job_template to create individual slurm scripts. For example, if scan 101 in Session 4 needs to run a Freesurfer pipeline, then DAX determines the status first and then builds a slurm script named “project_name-x-subject_name-x-4-101-x-FreeSurfer.slurm” that has all the requirements obtained from the yaml file(number of processors, walltime, memory,etc). DAX is also responsible for submitting this slurm script to ACCRE.
- Once DAX submits the job(sbatch .slurm), ACCRE queues the job request on the cluster and a node that satisfies the requirements of the slurm script would take up the job. Once the job is done, DAX checks the status of the job and uploads the results back to XNAT.
- We use a singularity container since we want the environment in our container to be preserved as such and not become obsolete when ACCRE decides to make an update on OS. Also, having the container enables us to install packages that will otherwise require making tickets for ACCRE to install them on the nodes.

## Step 1: Build a Singularity Container

There’s lots of options here. Pick your fave.

- Install singularity 3+ on your machine if it’s not already.
  - NB: ACCRE no longer supports singularity v2.
- Build an Ubuntu singularity sandbox from DockerHub
- Install your scripts.

## Step 2: Write a YAML File

[YAML Documentation](https://dax.readthedocs.io/en/latest/processors_v3.html)

## Q&A

### Is it necessary that my singularity take a directory as an input, or does providing a filepath also work? When the spider is running, is it assumed there is only 1 file in the directory?

- I recommend using a directory as input since using files in the root of singularity has posed problems in the past.
- It depends. If all you need is one NIFTI file as input to your container, then the INPUT directory would have just the NIFTI image in it. If you need multiple directories as input for your container, then all of them will be inside your INPUT directory.

### So my specific use case is segmentation of a single NIFTI file. My singularity container will take an INPUT directory and assume there is a single nifti file in it, process it, and write the outputs to the OUTPUT directory. If this spider is run on DAX and, say we want to apply it to all the CTs on XNAT, are my assumptions okay?

- This assumption is correct. For each scan on XNAT, a separate job would be run. Therefore, it would be a job per scan.

### Is the YAML needed on a case-by-case basis, or should I provide a generic one for the singularity container?

- I think YAML file should provide a generic argument for running the singularity container. The deep lesion code also used YAML as a config file to input different arguments for running the training and testing. You can use it as an example to take a look in the masi github.

### Which fields should I create/use to specify requested GPUs for slurm? eg: if Slurm provides the limit on visibility, is it my responsibility to provide a formatted YAML to do this?

- We use 1 by default and it is defined in the job_template_gpu file.

### How are GPUs and nodes related? My script currently takes a GPU ID number and uses that GPU for segmentation. If I don’t provide it, it tries to use all visible GPUs. If I set this to just be a boolean flag, GPU_YES / NO, will it only see a single GPU available for that node/session, or all GPUs available, or is this a different setting

- We have a separate slurm job template for GPU jobs where we request for a single GPU on an available node.
- You can’t do all available GPU on a node. You would have to specify the number of GPUs. If you want to run your job without GPU, then it needs a different yaml processor which would use the regular slurm job template( ! gpu job template)
- [GPUs, Parallel Processing, and Job Arrays](https://www.vanderbilt.edu/accre/documentation/parallel/)

### So I can limit the GPU visibility with the YAML file?

- Slurm will provide the limit on visibility. I have asked Brian Boyd about whether dax allows users to change the number of gpu’s without having to modify the gpu job template. I am guessing you only need one GPU but it would be nice to know that we can provide an easy option for multiple GPU usage.

### Are there any example spiders I can look at?

- [MATLAB FSL Demo](https://github.com/VUIIS/demo-singularity-matlab-fsl)
- [SPM Demo](https://github.com/VUIIS/demo-singularity-spm-freeview)
