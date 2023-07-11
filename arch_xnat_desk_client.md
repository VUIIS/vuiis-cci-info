# Uploading to Arch XNAT Using the Desktop Client

To upload data to [Arch XNAT](https://arch.xnat.vanderbilt.edu/xnat/), we will use the [XNAT Desktop Client](https://www.xnat.org/download/desktop-client/). Before uploading data, the project will need to exist. There is a walkthrough here: [Creating a New XNAT Project](https://www.xnat.org/download/desktop-client/).

Once the project is created and the XNAT Desktop Client downloaded, navigate to the Desktop Client GUI and click 'ADD NEW XNAT SERVER'. 
- For the server, enter in **arch.xnat.vanderbilt.edu/xnat**
- The username/password should be your login information for Arch XNAT.
- Once logged in, click 'Upload files'
- Select your project from the project list
  - Once you select a project, you should get some information about the project
- Select the DICOMs directory or file that you want to upload to the project
- Hit 'Next >'
- You will now see a list of all the patients and DICOMs
  - You can now select how you want the Subject labeled
    - Manually
    - Auto-Generate
    - Using Patient Name
    - Using Patient ID
  - You can also select how you want the Session labeled
    - Auto-Generate based on Subject label
    - Using Accession Number
    - Using Patient ID
- Hit 'Next >'
- Now you will have the ability to review the images
- When done, hit 'Finish and Upload'
- The uploading will now start and you will get display of the status
