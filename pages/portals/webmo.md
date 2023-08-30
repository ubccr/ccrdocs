# WebMO

WebMO is a web-based interface to computational chemistry packages.  The WebMO portals provided by CCR include access to Gaussian.  The JAVA molecular editor provides an easy interface for model building.  

## Access to WebMO

There are two types of WebMO instances available at CCR:  

**Research Groups:**  To request access for your research group or department, please request an allocation for the `WebMO (server)` resource in [ColdFront](https://coldfront.ccr.buffalo.edu).  CCR staff will contact the PI to discuss the anticipated usage by their group in order to appropriately size the cloud instance and provide a cost for the year.  Our prices are based off the [Lake Effect cloud pricing](../cloud/lake-effect.md).  Once the payment is received by CCR, the allocation will be activated and the PI (or trusted group member) will be provided with an administrator acccount to create accounts for their group.  Instructions for user management can be found in the [WebMO documentation](https://www.webmo.net/link/help/UserManager.html).  In order to keep the instance in service for your group, you must renew the allocation and payment annually.  

**Academic Courses:**  To request a WebMO instance for your course, please submit a ticket to [CCR Help](../help.md) **at least two weeks prior to the start of the semester**.  There is no cost for academic usage of WebMO at CCR.  CCR will create a WebMO instance for the class and provide the professor (or trusted TA) with an administrator account to create accounts for their students.  Instructions for user management can be found in the [WebMO documentation](https://www.webmo.net/link/help/UserManager.html).  At the end of the semester, the WebMO instance will be removed from service by CCR.    

!!! Warning "Gaussian License Restrictions"   
    The University at Buffalo owns a restricted license for Gaussian use on campus.  **The use of this software is permitted for faculty, staff, and students of the University at Buffalo ONLY.  Do NOT provide access to this software to anyone NOT officially affiliated with the University at Buffalo or you risk UB losing access to this license entirely.**  If you are unsure what "affiliated" specifically means for this software license, please contact [CCR Help](../help.md) to be connected with the person who manages this license for UB.

## Logging into WebMO  

WebMO accounts are created by your research group leader or your class professor or TA.  Please contact them for your group's portal URL and login instructions.  

## WebMO Documentation  

Please refer to the [WebMO Documentation](http://www.webmo.net/download/WebMO_Users_Guide.pdf) for guidance.  

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
