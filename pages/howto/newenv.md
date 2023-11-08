# CCR's Software Environments Explained  

CCR is now releasing [standard software environments](../software/releases.md) which
provide users access to a large suite of software programs, libraries, and
toolchains supporting all types of workloads across our [clusters](../hpc/clusters.md).
This page is intended to provide details on changes users can expect and tips
for a smooth transition.

Beginning August 31, 2023 CCR staff will host weekly office hours via zoom from
11am-12pm on Thursdays to provide support to users switching over to the new
environment.  Please join us and bring your questions:

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
- `ccrcsoft/2023.01` This is the latest CCR software release

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

## How to use the legacy software?

`ccrsoft/legacy` is now deprecated and users are encouraged to transition to
the latest release. If you need to use the legacy software environment  during
this transition period here are a few tips:

- Ensure all your jobs have the `--constraint=LEGACY`
- Load this module: `ccrsoft/legacy`
- If required, set this as your default by running:
  ```
  echo "module-version ccrsoft/legacy default" >> $HOME/.modulerc
  ```

!!! Warning "Default version changing soon"
    The latest software environment `ccrsoft/2023.01` will be loaded by default
    starting after the December 2023 maintenance downtime. Users are encouraged
    to migrate all workflows to `ccrsoft/2023.01` as soon as possible

## How to use new compute resources?

CCR recently deployed brand new compute resources with new processors, memory,
and GPUs. These nodes have been temporarily put into a reservation for users to
access them and starting after the December 2023 maintenance downtime you will
no longer need to specify the reservation. 

Currently, you will need to specify the following in your batch scripts: 

```
#SBATCH --cluster=ub-hpc
#SBATCH --partition=general-compute
#SBATCH --qos=general-compute
#SBATCH --reservation=ubhpc-future

module load ccrsoft/2023.01
```

!!! Tip "Use the latest ccrsoft/2023.01"  
    These new nodes work best if using the latest ccrsoft release. 

## New login node vortex-future is... the future?

Users now have access to a new login node: `vortex-future.ccr.buffalo.edu`.
This login node will always contain the latest and greatest features CCR has to
offer and serves as a preview of the next deployment of all login nodes. 

## New version of OnDemand?

We have deployed the new version of OnDemand version 3.0 available [here](https://ondemand.ccr.buffalo.edu).
There are many new features to take advantage of, as well as changes to how we've laid out the apps.
Please [see here](../portals/ood.md) for more details.

## I'm getting "Module command errors"?  

- Try adding: `--constraint=AVX512` to your job script.
- Ensure the first line of your script is: `#!/bin/bash -l`

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
