# UBMoD Metrics Portal  

CCR is pleased to provide users with UBMoD - the Open XDMoD web-based tool for monitoring machine utilization and retrieving job statistics.  The interface provides a dashboard overview of resource consumption along with fine-grained control over the time period and resources that are displayed. The information is presented in easy to understand interactive charts, graphs, and tables.


## Login to CCR's UBMoD Portal  

!!! Warning "VPN Required"
    Access to UBMoD is restricted to UB and Roswell Park networks
    (either on campus or connected to their VPN services). [See here](../getting-access.md#vpn-access)  

Login to [UBMoD](https://ubmod.ccr.buffalo.edu) with your CCR account.  Don't have one yet? [see here](../getting-access.md)


## Where does the information come from?
The information is harvested from the SLURM accounting log files. The workload manager logs various bits of information about each job throughout it's life cycle. Each night these log files are processed and the data is aggregated and stored in a database.

## How often is the information updated?
The job stats are updated nightly and aggregate the data on a rolling week (last 7 days), month (last 30 days), and quarter (last 84 days). The web interface displays the information as of the previous day.

**More UBMoD documentation coming soon!**
