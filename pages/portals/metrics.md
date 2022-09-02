# Open XDMoD Metrics Portal  

CCR is pleased to provide users with a web-based tool for monitoring machine utilization and retrieving job statistics.  The interface provides a dashboard overview of resource consumption along with fine-grained control over the time period and resources that are displayed. The information is presented in easy to understand interactive charts, graphs, and tables.


## Login to CCR's Open XDMoD Portal  

https://metrics.ccr.buffalo.edu  

!!! Warning  
    You must be on the UB campus or connected to the [UB VPN](https://buffalo.edu/ubit) from off campus in order to access CCR's portals  

Two factor authentication must be enabled on your CCR account in order to access CCR's OnDemand portal.  If you do not, you will get the error ``You don't have access to this resource`` when attempting to login.  

If you get the error ``invalid login`` you are entering your password, one-time token from your authentication app, or both incorrectly.  

Having trouble with 2FA?  Watch this 50 second video!  
![type:video](https://www.youtube.com/embed/g6hWYooFKWE)

[More information on two factor authentication](../2fa.md)  


### Where does the information come from?
The information is harvested from the SLURM accounting log files. The workload manager logs various bits of information about each job throughout it's life cycle. Each night these log files are processed and the data is aggregated and stored in a database.

### How often is the information updated?
The job stats are updated nightly and aggregate the data on a rolling week (last 7 days), month (last 30 days), and quarter (last 84 days). The web interface displays the information as of the previous day.

### More XDMoD documentation coming soon!
