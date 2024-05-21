# Assessor statuses

How to view:

- Bottom of the session page
- The Processing tab on the project page
- DAX command line tools:
  - Xnatinfo for summary
  - Xnatreport for details
  - Xnatreport_assessors for even more details


**NEED_INPUTS**: Waiting on dependencies and will run automatically when they are available. Could be a scan or assessor resource not available, a prerequisite assessor that hasn't completed, or a QA/QC status field that hasn't been set.

**JOB_RUNNING**: Set when the job has been sent to the cluster. On the cluster itself the job could be pending, running, or complete - the specific status on the cluster is not viewable on XNAT. This status may last a few hours up to two weeks, depending on how busy the cluster is and how long the job takes to run.

**UPLOADING**: The job has completed on the cluster and results are being loaded back to XNAT. This status should be brief - if it lasts more than a day, a process on the cluster has probably crashed and needs admin help.

**COMPLETE**: Job has run to completion on the cluster and the results have been loaded back to XNAT.

**JOB_FAILED**: Job has run to completion on the cluster, but something went wrong and results are missing or incomplete on XNAT. Review the OUTLOG to find out what the problem was. The job will not re-run unless manually set to do so.

**NO_DATA**: Some prerequisite was missing when the job was last built, and the job will NOT automatically re-run unless manually set to do so.

