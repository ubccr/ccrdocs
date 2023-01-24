# WebMO

WebMO is a web-based interface to computational chemistry packages.

The WebMO portal provides access to GAMESS, NWChem, and GAUSSIAN (license restricted).  The JAVA molecular editor provides an easy interface for model building.  WebMO is integrated with the UB-HPC cluster and several partitions in the Faculty cluster.  The user jobs are automatically submitted to the cluster selected in the WebMO job.

## Access to WebMO

A CCR system account and an active allocation to WebMO is required.  [Allocations are managed in ColdFront](coldfront.md) by faculty group leaders or principal investigators  


!!! Warning  
    You must be on the UB campus or connected to the [UB VPN](https://buffalo.edu/ubit) from off campus in order to access CCR's portals  

## Logging into WebMO  

WebMO accounts use your CCR system account and two factor authentication.

[Access CCR's WebMO portal here](https://webmo.ccr.buffalo.edu/~webmo/cgi-bin/webmo/login.cgi)

!!! Note "Special Login Procedure!"
    Logins require password plus the one-time token (OTP) generated from your authentication app.  These are entered back to back with no spaces or extra characters between them.  For example:  
    Password: BuffaloLove!  
    OTP code displayed: 123 456  
    Enter in the WebMO password box:  BuffaloLove!123456  

## WebMO Documentation  

CCR staff are unable to provide assistance in using WebMO.  Please refer to the [WebMO Documentation](http://www.webmo.net/download/WebMO_Users_Guide.pdf) for guidance.  

## Data Management with WebMO  

The files WebMO generates can be quite large. To clean up your disk usage, you will need to login to the WebMO interface and remove jobs.  

### Download Job Archives  

If you'd like to retain the files, you can export the job files and save them to your local computer.  

<ol>
<li>Click on the check box next to the job(s) you'd like to download  
<li>Click on the arrow next to the Download button at the top and choose "Job Archive"  
<li>A new file should be downloaded to your computer named "archive<jobnumber>.tar"  
</ol>

### Delete Unwanted Job Files  

<ol>
<li>Click on the check box next to the job(s) you want to delete
<li>Click the Delete button at the top
<li>Click on the "Trash" link on the left side to see what you've marked for deletion
<li>Click the "Empty trash" link on the left to permanently delete the files from the server.  NOTE: if you do not empty the trash, the files will remain on the filesystem thus your disk usage will remain unchanged and your quota will continue to report that usage.
</ol>
