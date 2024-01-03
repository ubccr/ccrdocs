# CCR's Software Environments Explained  

CCR is now releasing [standard software environments](../software/releases.md) which
provide users access to a large suite of software programs, libraries, and
toolchains supporting all types of workloads across our [clusters](../hpc/clusters.md).
This page is intended to provide details on changes users can expect and tips
for a smooth transition.

CCR staff host weekly office hours via zoom from
11am-12pm on Thursdays to provide support to users switching over to the new
software release.  Please join us and bring your questions:

```
https://buffalo.zoom.us/j/94613848883?pwd=Q2ZjU3VIaWZDZGZPdldjR1JwOUVmZz09 
Meeting ID: 946 1384 8883 
Passcode: 497161 
```

## What are standard software environments?

More details [see here](../software/releases.md).

## What versions are available?

As of this writing there are 2 releases of ccrsoft:

- `ccrsoft/legacy` This is the legacy CCR software release and is now deprecated. 
- `ccrcsoft/2023.01` This is the latest CCR software release and the default.

## How to use the latest ccrsoft release?

When you login the default version of ccrsoft is loaded automatically. To use a
specific version you can run:

```
$ module load ccrsoft/2023.01
```

To configure a specific version as the default for your user account you can
set the default version in your `~/.modulerc` file. For example: 

```
$ echo "module-version ccrsoft/2023.01 default" >> $HOME/.modulerc
```

**NOTE: User accounts created after August 8, 2023 have the .modulerc file created automatically and is set to the latest software release.**  


## How to use the legacy software?

`ccrsoft/legacy` is now deprecated and users are encouraged to transition to
the latest release. If you need to use the legacy software environment during
this transition period here are a few tips:

- Ensure all your jobs use the `--constraint=LEGACY` in the batch script or interactive job request
- When using OnDemand apps, use one of the Legacy apps or specify `LEGACY` in the "Node Features" box of the app form
- Load this module prior to loading any of your other modules: `ccrsoft/legacy`
- If desired, set the legacy environment as your default by running:
  ```
  echo "module-version ccrsoft/legacy default" >> $HOME/.modulerc
  ```

!!! Warning "Default version is now ccrsoft/2023.01!"
    As of the January 2024 maintenance downtime, the latest software environment `ccrsoft/2023.01` will be loaded by default on all CCR login and compute nodes.  To continue to use the legacy software, you MUST make the changes listed above.  Users are encouraged to migrate all workflows to `ccrsoft/2023.01` as the legacy modules are no longer supported and will be completely removed from CCR systems as of June 2024.

## How to properly request GPU nodes?

CCR recently deployed brand new compute resources with new processors, memory,
and GPUs.   The new GPU nodes have the latest NVIDIA drivers installed on them and should be used with the latest software release. To ensure your job gets allocated on a newer GPU node, we recommend specifying `--constraint=NONLEGACY` in your Slurm job script or in your interactive session request.  If using OnDemand, you can specify `NONLEGACY` in the "Node Features" box of the application forms.

 For more info on requesting GPUs [see here](../hpc/jobs.md#slurm-directives-partitions--qos):  


!!! Tip "Use the latest software environment for GPU use"  
    Legacy software can not be used with the new nodes due to driver incompatibilities.  If you must use legacy software, use the `LEGACY` constraint when requesting a GPU.     

## New login node vortex-future is... the future?

Users now have access to a new login node: `vortex-future.ccr.buffalo.edu`.
This login node will always contain the latest and greatest features CCR has to
offer and serves as a preview of the next deployment of all login nodes.  You may continue to use `vortex.ccr.buffalo.edu` which loads the default ccrsoft\2023.01 software release as well.  

## New version of OnDemand?

We have deployed the new version of OnDemand version 3.0 available [here](https://ondemand.ccr.buffalo.edu).
There are many new features to take advantage of, as well as changes to how we've laid out the apps.
Please [see here](../portals/ood.md) for more details.  Users may notice some changes with the way desktop sessions act:  

  - The desktop takes longer to draw on the screen after launching the session.  This is the new normal.  It may take 1-2 minutes for the desktop to draw and icons to display.  
  - Sometimes the icons don't work or aren't displaying correctly.  [See here](../faq.md#why-do-i-see-a-blank-window-when-starting-an-ondemand-desktop-why-are-the-desktop-icons-not-working) for guidance.  
  - Users that want to continue to access applications in the ccrsoft/legacy software release should use the OnDemand apps marked LEGACY.  There is a _LEGACY - UB-HPC & Faculty Cluster Desktop_ app and a _LEGACY - Jupyter Notebook_ app  
  - The LEGACY Jupyter and UB-HPC & Faculty Cluster Desktop apps will be removed from service along with the ccrsoft/legacy software release in June 2024.  

## I'm getting "Module command errors"?  

- Ensure the first line of your batch script is: `#!/bin/bash -l`
- There are older nodes in the faculty cluster with AVX2 CPU architecture.  Not all software has been built for these CPUs.  Add: `--constraint=AVX512` to your job script or interactive session request to ensure your job runs on a supported CPU.  If using OnDemand, specify `AVX512` in the "Node Features" box of the application form.


## What if we install our own software?

If you install/compile your own software you will need to rebuild using the
latest `ccrsoft/2023.01` release. We encourage users to checkout easybuild and
our docs on [building your own software](../software/building.md).

## Software Installation Requests?

CCR is accepting requests for software installations and encourages users to
"like" any requests they see for software they want to use in [this list](https://github.com/ubccr/software-layer/issues).
This helps us to rank the requests and prioritize the order they are installed. 
[Follow these instructions](../software/building.md#software-build-requests) to request a
software build. 
