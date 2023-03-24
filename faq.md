# FAQ

## FAQ

### Starting spiders on a new project

On all new projects, share the data into subprojects and run spiders from the subprojects. This will help you avoid issues with running projects directly on your ‘PI-NAME’ project. For an example, look at the following:

- PI Name: John Johnson
- Head project: JOHNSON
- Subproject: JOHNSON_XXXXX

All scans should go to the JOHNSON project, and scans would then need to be shared with the JOHNSON_XXXXX project. Then run the spiders on the JOHNSON_XXXXX project.

### Setting up a new XNAT account

1. Navigate to the XNAT entry page at https://xnat.vanderbilt.edu/xnat
2. Click “Register” to request a new account. Choose your username and a *unique* password. This is separate from VU/VUMC systems, so do not re-use your VU/VUMC passwords. VU/VUMC members should provide their vanderbilt.edu or vumc.org email address.
3. You will receive an email from vuiiscci-admin@vanderbilt.edu asking you to verify your email address.
4. After email verification, your account request will be reviewed manually, usually within a day or two. You (or your PI) will receive an email requesting confirmation of your access.
5. You will receive a welcome email from vuiiscci-admin@vanderbilt.edu. At this point you must log in at https://xnat.vanderbilt.edu/xnat/ to activate your account.
6. Once you have logged in, project owners will be able to grant you access to specific projects as desired. If you are a project owner (e.g. VU/VUMC PIs), you can navigate to your project’s “Access” tab to manage this.

### Some scan data are missing

Scans coming in from PACS go through the pre-archive. In most cases they will then proceed to show up in the usual place in a subject record without any handholding. But sometimes, due to project settings or timeout issues during communication with PACS, a study or some scans in a study will get stuck in the pre-archive and not show up where expected. To investigate:

- Go to XNAT web page
- Go to Uploads menu in the top blue bar and select “Go to prearchive”
- Look for your scan in the list:
  - Not there, or has “Error” status? Contact us to resend from PACS.
  - Has “Receiving” or “Building” status? If it’s been a day since the scan, select the study’s checkbox and click “Rebuild” on the far right. Check again in a few hours.
  - Has “Conflict” or “Ready” status? Select the study’s checkbox and click “Review and Archive” on the far right. On the new page, don’t edit anything. Simply click “Submit” at the bottom. It is generally ok to ignore or click through any warnings about things already existing. Archiving might take an hour or so.

### Dealing with multiple, same name scans before processing

- If you know a specific scan is incomplete or inadequate quality, mark it 'unusable' in XNAT so it will be ignored in processing. This is the main mechanism for choosing which scans to use. 
  - If there is more than one relevant scan is a session that is NOT marked 'unusable', automatic selection is reliable, but limited. The FIRST or LAST available matching scan can be selected, but this setting applies across the entire project and CANNOT be changed mid-stream without generating major issues. 
  - If needing more information, the engineers can run an assessor on individual scans to give a preliminary set of reports for review. When there are a lot of cases with mulitiple potentially usable repeat scans, this is where to start..
- Generally, deleting a scan from XNAT (but never from PACS) would be a last resort

### Setting quality status

To mark multiple scans Usable/Unusable:

- Use the Xnatreport and Xnatsetvar command line tools in dax

To mark a single scan, e.g. Usable/Unusable:

- Go the session page
- Edit button in Actions menu (black text, at the right side)
- Change the Quality setting for the relevant scan (but don’t change anything else)
- Press blue Submit button at the bottom

To mark a single assessor, e.g. Passed/Good/Bad:

- Go to the assessor page
- Edit button in Actions menu
- Update the “Status”
- Press Submit

### Restarting a failed job

A job’s outlog is usually helpful to distinguish whether a failure is due to a problem with the data, or a momentary problems or downtime with XNAT or ACCRE. If the latter, it just needs to be restarted. A job can be restarted via the XNAT web interface:

- Go to the assessor page, e.g. by clicking on the assessor name in the ProcID column under Processing on the session page
- Click Edit button in Actions menu to the right
- Under Status, select **Rerun**
- Click Submit at the bottom

This usually takes effect within a few hours – the assessor status will change to NEED_INPUTS, then the job will re-enter the queue as usual. A restart may take longer for projects with large or complex pipelines set up.

### Deleting things on XNAT

Be careful, obviously. The original scan data can generally be re-acquired from PACS. Assessor/processor results and any files that have been uploaded from some other source, like manual segmentations, could be gone forever. Assessors can easily be re-run, but some have random initializations and don’t produce quite identical results every time. To delete a single resource or file of a scan (e.g. delete the NIFTI so it can be recreated, without deleting the DICOM):
- Go to the session page
- Manage Files button in Actions menu (black text, right side)
- Find the specific resource or file and click the red trash can icon

To delete an existing scan:
- Go the session page
- Edit button in Actions menu (black text, at the right side)
- Press the little trash can icon beside the specific scan

To delete an existing assessor:
- Go to the assessor page
- Delete button in Actions menu

To delete an entire session or subject:
- Go to the session or subject page
- Delete button in Actions menu


### My job says NEED_INPUTS. What does this mean?

One of two things:
1. A requirement for the spider to run has not been met. Some required data may be missing (a necessary previous assessor hasn’t finished or a necessary scan is missing). This also happens when an earlier scan or process needs a specific Quality or QC setting before the assessor will run.
2. The status may have just been reset after a previous job failure, and the change hasn’t been noticed yet by DAX. These usually get noticed within a day or two unless there are extenuating circumstances, like XNAT being down for a while. A project with an especially large number of assessors running may take several days to update.

### Why did my job fail?

There are many reasons why a job could fail including but not limited to walltime and memory were set too low, data quality was low, registration (if necessary) failed, etc. A great place to start to figure out what happened, is to check the OUTLOG resource for the process. This contains the STDOUT and STDERR of a spider and anything that ran inside it (unless redirected to a separate text file). Anything in here that says kill or ERROR are great places to check. If that doesn’t work, you can click on the assessor label on XNAT. One of the variables you will see is “job id”. If you run the command stracejob <jobid> on ACCRE, it will tell you what node the job failed on. You can then log in and see what happened on the specific machine (all data remain there for several days).

### Where do I see what command ran?
  
The PBS resource is the exact shell script that is executed on ACCRE.  

### What is DAX?

Distributed Automation on XNAT (DAX) is a software package written by the MASI lab. It is build on top of XNAT and installed on gateways and personal computers (*NIX complaint). It is a sandbox of tools for managing and launching jobs on a gird, downloading and uploading data XNAT, and controlling process status
  
### What is a Spider?
  
A spider is an encapsulated pipeline that handles the downloading of outputs, running an image processing algorithm, producing a QA PDF and sorting outputs into folders, which in XNAT terms, are referred to as “resources”
  
### How are spiders configured?

Settings for each spider such as software path(s) scan type(s) to run on are stored in REDCap and “turned on” for an entire project. Thus spiders are not run on individual sessions, but across the entire project.
  
### My spider failed and I don’t know why. What should I do?
  
#### Verify Scan Input is Setup Correctly
  
If the container is looking for scan_t1’s fdest resource to be ‘t1.nii.gz’ as input, verify that the value isn’t something like ‘T1.nii.gz’. Capitalization matters!
  
#### Verify Attribute Input is Setup Correctly
  
Usually attributes, if used, follow similar layouts as below
```
      - varname: project
        object: session
        attr: project
      - varname: subject
        object: session
        attr: subject_label
      - varname: session
        object: session
        attr: label
      - varname: t1_scan
        object: scan
        attr: ID
        ref: scan_t1
      - varname: dwmri_res
        object: assessor
        attr: label
        ref: assr_dtiqa
```
Where scan objects have an attr of ID, while assessor objects are label.
  
#### Outputs are Correctly Setup
  
For instance, the path variable may be setup as a FILE type. Make sure this is correct. Also, if the container pulls a PDF file from somewhere like DIRECTORY_1/DIRECTORY_2/*.PDF, then the path should include those directory names. Make sure that output file names match across the processor and YAML file.
  
#### Verify Singularity Execute Script has Correct Number of Inputs
  
Singularity Inputs should match the number being passed in the processor file.
  
#### Last to Try
  
If all else fails, email masi-admin@list.vanderbilt.edu. There are about 10 people on this mailing list that actively monitor job processing statuses.
  
### How do I write a spider?
  
If you have questions on how it works, email masi-admin@list.vanderbilt.edu for an example or tutorial.
  
### My job appears to be stuck in the same status for several days? What should I do?
  
Depending on the process that is running, a lot of things could have happened. The job could be held in queue on ACCRE’s end, the process could take a few days, or the process could be in the queue to be uploaded. All of these will be denoted by JOB_RUNNING in XNAT.
  
### How do I test a spider?
  
We have a sandbox account hooked into (read only) our production environment. You are welcome to use this to test writing your own spiders. We also have a Development XNAT instance if you are curious in testing out before running on our production software and hardware.
  
### I’m new. Where should I even begin?
  
The following lists a subset of opportunities available at Vanderbilt for students, post docs, and trainees.
  
#### Center for Computational Imaging
  
- Annual Introduction to the CCI
  - The VUIIS Center for Computational Imaging (CCI), a part of the Human Imaging Core, is offering an overview of capabilities and ongoing efforts during the PNP Seminar.
- Readthedocs
  - Current installation procedures are on [readthedocs](https://dax.readthedocs.io/en/latest/installing_dax_in_a_virtual_environment.html). Please follow the install instructions there rather than the videos. The videos do provide a good overview and are also useful.
- Engineering Support and Meetings
  - We operate a support e-mail list (vuiis-cci@googlegroups.com).
  - We have engineering meetings Fridays 9am-10am — all are welcome.
    - All of the engineering staff attends and it’s a great place to bounce off new ideas and help troubleshoot project-specific issues.
  
#### Vanderbilt Courses
  
- EECE 6358. Quantitative Medical Image Analysis.
  - Image processing and statistical methods for quantitative analysis and interpretation of medical imaging data. Neuroimaging approaches related to brain structure, function, and connectivity. Massively univariate analysis (parametric mapping), multiple comparison issues, random fields, independent components, non-parametric approaches, and Monte Carlo methods. Students should have knowledge of undergraduate probability and computer programming. [3]
- NSC 3270/NSC 5270. Computational Neuroscience. [Formerly NSC 270]
  - Theoretical, mathematical, and simulation models of neurons, neural networks, or brain systems. Computational approaches to analyzing and understanding data such as neurophysiological, electrophysiological, or brain imaging. Demonstrations simulating neural models. Prerequisite: 2201, either CS 1101 or 1103, and either MATH 1200 or 1300. [3] (MNS)
- PSY-PC 2230. Introduction to Educational Neuroscience.
  - Educational neuroscience (ed neuro) is an emerging scientific field that investigates how the brain enables learning. Ed neuro applies the methods of cognitive neuroscience to questions such as what are the brain systems that allow us to read and do math? How do those systems relate to general systems such as attention and memory? This course will provide an introduction to these topics and more, exploring the basics of how the brain is structured, to how we can use neuroimaging methods to understanding the brain structures and processes that support learning. At the end of this course you will have a basic understanding of cognitive neuroscience methods and how they relate to educationally relevant cognitive domains. [3]
- PSY 8216. Brain Imaging Methods. [Formerly PSY 316]
  - Principles and methods used in human neuroimaging, with emphasis on functional magnetic resonance imaging (fMRI). [3]
  
#### Outside Vanderbilt
  
- Continuing Education at the Martinos Center
  - http://www.martinos.org/martinos/training/index.php
  
### Are there any mailing lists or google groups I can follow?
  
YES! We have a mailing list that we always report downtimes to. Email bennett.landman@vanderbilt.edu to get added or add yourself [here](https://groups.google.com/g/vuiis-cci/members).
  
### I have A LOT of data that I would like to upload and run processes on. What should I do?
  
Please email bennett.landman@vanderbilt.edu with a brief summary of the data. VUIIS will need to formally approve the addition of the data to the VUIIS XNAT. We (might) already have uploaded the data ourselves. There are over 300 active projects in the VUIIS XNAT archive. Please limit your upload to no more than 2 instances at once. The VUIIS XNAT is a shared resource and overloading it can cause unexpected run behavior.
  
### I think I found a bug what should I do?
  
Our bug tracker is available here: http://xnatbug.vandyxnat.org/bugzilla/
  
### Is there any documentation for DAX?
 
Yes. The canonical docs are available here: http://dax.readthedocs.io/en/stable/
  
### I have a ton of DICOM data. Is there an easy way to send to your XNAT?
  
Yes! XNAT has a built in DICOM receiver which is easy to use. Check out our documentation here: [Sending DICOM to Vanderbilt XNAT](XNAT/sending_dicom_to_xnat.md)
  
### I have a ton of non-DICOM data. Is there another easy way to send to your XNAT?
  
Yes! Xnatmirror (part of DAX) was designed for just this purpose. It will copy a project from one instance to another. Or, Xnatupload may be used for data not already in an XNAT.
  
### What is the procstatus?
  
Procstatus is use by DAX to indicate the status of an assessor. There are various strings that can be put here. Below is a list of them:
- COMPLETE – The spider finished as expected. All outputs are there.
- JOB_FAILED – The spider finished abnormally. Usually this means that there was an error during the image processing algorithm. Other reasons include running over time limit, the user doesn’t have access to the project, a path doesn’t exist, etc.
- NEED_INPUTS – As mentioned above some of the jobs require previous processes to be qc’d to run. This is the most frequent case for this status.
- JOB_RUNNING – The processor has indicated that all of the spider’s dependencies are met. At this point the job has been submitted to the grid. The job may be in queue for a day or two depending on how many jobs are running at the current moment, but it will move its way up in priority depending on how long it waits.
- NO_DATA – This means that a scan is most likely missing (or a previous process failed that is required for the current one to run). These will be skipped over in DAX once set to NO_DATA
  
## NIFTI Information
  
### NIFTI CONVERSION
  
Nifti files for VUIIS scans can be obtained via on-the-fly conversion from gstudy (http://vuiis.vumc.org/gstudy). The simplest and most likely to work is gstudy’s “dcm2niix” version of the nifti converter – a recent version that works with most Philips DICOMs.

If you have already downloaded all the DICOMs, or you have an exam card that gstudy doesn’t convert properly, it’s probably easier to install the newest dcm2niix yourself:
https://github.com/rordenlab/dcm2niix/releases

All versions of dcm2niix are also available within VUIIS XNAT.
  
### DIFFUSION IMAGING
  
Different nifti converters produce different b-vectors. Some older converters output b-vectors in the DICOM coordinate frame, which is often not what is needed. Recent versions of dcm2niix output b-vectors in the voxel coordinate frame, which is what’s needed for FSL or MRTrix.
  
### NIFTI AND MATLAB
  
This popular matlab nifti toolbox (load_nii etc) is buggy, and no longer maintained. It can introduce geometry, positioning, and coregistration errors in nifti files: https://www.mathworks.com/matlabcentral/fileexchange/8797-tools-for-nifti-and-analyze-image

The errors can usually be fixed after the fact with FSL tools, but that takes experimentation and is error-prone. There is not a great alternative for reading and writing nifti files in matlab, but here is one possibility: https://github.com/VUIIS/spm_readwrite_nii
  
## Get Started with REDCap Report Generation
  
The redcap_report_generator is a tool that facilitates automation of report generation in word document format ‘docx’.
  
### Installation

```  
$ pip install redcap_report_generator
```
  
Prerequisites are PyCap, argparse and docx modules. Pip automatically checks and installs these packages. To upgrade to newer versions:
```
$ pip install --upgrade redcap_report_generator
```
  
Or with git:
```
$ git clone https://github.com/KarthikMasi/redcap_report_generator.git
$ cd redcap_report_generator
$ sudo python setup.py install
```
  
### Template Document
  
redcap_report_generator requires a template document to be provided under argument -f. The template document has to contain the fields from REDCap that needs to be replaced in the report.
  
#### Help
 
```  
$ redcap_report_generate -k {REDCap API KEY} -r {FIELDS} -f {PATH TO TEMPLATE 
     DOCUMENT} -p {PARTICIPANT_ID} -d {DESTINATION FOR WORD FILE TO BE 
     SAVED} -u {FIELD NAME FOR FILE UPLOAD}

usage: redcap_report_generate [-h] [-k REDCAP_KEY] [-r REPLACEMENT] [-f FILE] 
      [-p PARTICIPANT_ID] [-d DESTINATION] [-u UPLOAD] [-e EVENT] [--ue UEVENT]
REDCap Report Generator
optional arguments:
 -h, --help            show this help message and exit
 -k REDCAP_KEY, --key REDCAP_KEY
                       Redcap API Token
 -r REPLACEMENT, --replace REPLACEMENT
                       words to be replaced
 -f FILE, --file FILE  Path to template document
 -p PARTICIPANT_ID, --participant PARTICIPANT_ID
                       Participant Id
 -d DESTINATION, --dest DESTINATION
                       Destination for output files
 -u UPLOAD, --uploadTo UPLOAD
                       Redcap field where generated document is to be
                       uploaded to
 -e EVENT, --event_name EVENT
                       event name in longitudinal studies only. Supports
                       multiple events
 --ue UEVENT, --upload_event_name UEVENT
                       Event name for upload option
```
  
To get help on terminal, type
```
$ redcap_report_generate --help
```
  
#### Example
  
The template document created by the user should contain the variable name in place of the field that needs to be fetched from REDCap form. Example template document:
```
Name: 	dl_first_name dl_last_name
Date of Birth:  dl_dob
Age: dl_age
Date of Evaluation: dl_date
```
  
This report shows his/her basic demography.
```
$ redcap_report_generate -k {REDCap API KEY} -r dl_first_name,dl_last_name,dl_dob,
     dl_date,dl_age -f {PATH TO TEMPLATE DOCUMENT} -p {PARTICIPANT_ID} -d 
     {DESTINATION FOR WORD FILE TO BE SAVED} -u {FIELD NAME FOR FILE 
     UPLOAD}
```

After running the above command, the document saved would contain the values corresponding to the records of the PARTICIPANT ID provided. Also, if a REDCap ‘file’ field is provided, the file shall be uploaded. Note that multiple comma separated PARTICIPANT IDs may be provided. Example output after running redcap_report_generator:
```
Name: 	John Doe
Date of Birth:  12/31/2000
Age: 17.3
Date of Evaluation: 2018/04/09
This report shows his basic demography.
```
  
The filename of the document would be the Participant ID provided(participant_id.docx). Also, note that redcap_report_generator can replace ‘his/her’ in your document with the appropriate replacement if gender of the participant is obtained in the REDCap form.
  
### Version Control
  
- redcap_report_generator-0.3.0: Version 0.3.0 supports longitudinal databases. Also has a check for sub-strings in tables. For eg: Consider field names ‘abc123’ ‘abc1234’ with values ‘0’ and ‘1’ on REDCap. Without sub-string check, results after running the tool would be ‘0’ and ’04’ respectively. This has been cleared out.
  - (redcap_report_generator-0.3.0 released on 09/11/18)
- redcap_report_generator-0.2.4: Version 0.2.4 includes an “import to REDCap field” option. The document generated with the redcap_report_generator can be uploaded back to a ‘file’ field on REDCap.
  - (redcap_report_generator-0.2.4 released on 04/24/2018)
  
## LDAX Modules

### Module_Auto_Archive  
  
The Auto Archive Module allows you to automatically move scans from the XNAT Prearchive into the Archive based on input from a REDCap database.

The REDCap database can be used to assign a Project ID, Subject ID, and Session ID that are different from those assigned on the scanner. Most sessions acquired on VUIIS scanners are initially assigned to a project using the last name of the PI. The initial Subject/Session numbers are based on an incrementing integer on the scanner. With the Auto Archive module, you can automatically archive scans and as part of the archive process, replace the scanner-assigned values with your preferred project names and IDs.

To use the Auto Archive module, you will need a separate REDCap project where you store a record for each MR session. This can be an existing REDCap database with a record per session or a longitudinal database with an event for each session.

The REDCap database should contain fields that store these specific pieces of data:
- Project (the preferred XNAT Project ID, must already exist in XNAT)
- Subject (the preferred subject ID)
- Session (the preferred session ID, should begin with the Subject)
- Session Date (the date the session was acquired, used for sanity checking, formatted as a REDCap date M-D-Y)
- VUIIS Session ID (the number assigned by the scanner)

The Auto Archive module can be configured to look in specific field names to find these data. If you are using a REDCap database in conjunction with dax_manager to configure your DAX projects, you can assign these field names there.
- Project Field (the name of the field containing the project ID)
- Subject Field (the name of the field containing the subject ID)
- Session Field (the name of the field containing the session ID)
- Session Date Field (the name of the field containing the session date)
- VUIIS Session ID Field (the name of the field containing the project ID)

In addition to configuring the field names for the session REDCap, you will also need to configure these parameters:
- API KEY (an environment variable containing the key)
- Prearchive Project (the Project ID the session is assigned in the Prearchive)
- Archive Project (the preferred Project ID you want to assign)
- Email address for errors (an email address to send any errors that occur while the module is running)

You can also optionally configure the Auto Archive module to use a longitudinal database by setting these parameters:
- Subject Event Name (the name of the REDCap event containing the Subject Field)
- Session Event Name (the name of the REDCap event containing the Fields for Session
- Session Date, Project, and VUIIS Session ID)

Note that the same REDCap project can be used for multiple XNAT projects. If you are using a REDCap database with dax_manager you will need to configure the Auto Archive Module for each XNAT project.

Contact: Brian D. Boyd

### Module_Autoseg_Leg

This is a half module, half spider. It generates an assessor and the entire process takes less than a minute to run
  
### Module_create_b0_scan
  
Module to create a b0 scan on XNAT – used to create dummy b0 for backwards compatibility with dtiQA_v5 and greater
  
### Module_dcm2nii
  
Module to generate NIFTI from DICOM with dcm2nii
  
### Module_Extract_physlog
  
Module to extract physlog from secondary files from Scanner 
  
### Module_Preview_Nifti
  
Module to generate the Preview for a scan from a resource (hosting NIFTI file)
  
### Module_Process_ROIs
  
Module to strip the skull from a structural scan on XNAT
  
### Module_Project_Summary
  
What processes this project is running (also show any custom settings)? What’s new this week? Sums of QA results: what needs to be done? What data can be analyzed? What’s running now? Are there outliers? What’s my average wml, fmri motion, hippocampus, etc? What’s in the prearchive? Count unique sessions for each scqa type in REDCap? Sessions from past week. Also, list anything currently stuck at JOB_FAILED. Each processor could display a description of itself and also show the average walltime and memory it’s using and how that compares to the requested walltime and memory. Each processor should display the bar chart of passed, failed, needed qa and then display boxplots of each output (or should we pick and choose which to display). Show what modules are enabled for this project.
  
### Module_Set_fMRI_Connectivity_Variables
  
‘The fmri connectivity spider requires two custom variables to be set at the scan level for each fmri scan. The variables are slorder and dropvols. While easy to set for studies that are no longer collecting data. This module accepts a json object to map sequence variant to the required variable key value pairs.
  
### Module_Set_Scan_Type
 
Module to set the scan type from a text file
  
### Module_set_voxel_res_and_fov
  
Module to generate NIFTI from phillips DICOM. Intermediate step: PARREC format.
  
### Module_Sync_Assessor_QC_To_Scan
  
Module to set the scan type from a text file
  
### Module_Sync_REDCap_All
  
Module to sync metrics from XNAT to REDCap
  
### Module_Sync_REDCap_ID
  
Module to sync metrics from XNAT to REDCap with the ID 
  
### Module_T1_skull_strip
  
Module to strip the skull from a structural scan on XNAT
  
### Module_Unique_Series_Description
  
Module to set the series description to a unique value
  
## DAX 1 Modules
  
### Module_Auto_Archive for DAX 1
  
Module to automatically archive sessions on XNAT following REDCap data
  
### Module_dcm2niix_bids
  
Module to generate NIFTI + JSON from DICOM with dcm2niix
  
### Module_dcm2niix
  
Module to generate NIFTI from DICOM with dcm2niix
  
### Module_parrec2niix
  
Module to generate NIFTI from parrec with dcm2niix
  
### Module_redcap_sync_yaml
  
Module to sync to REDCap
