# CPU Microarchitectures

CCR supports a wide variety of CPU Microarchitectures. All of our software is
compiled with specific optimizations enabled to take advantage of the various
features of each Microarchitecture. This section includes guidelines for running
on specific architectures including any additional steps required for successful
job submission. For more information on CPU Microarchitectures see here:

- [x86\_64 Microarchitecture Levels](https://en.wikipedia.org/wiki/X86-64#Microarchitecture_levels)
- [ARM Architecture Family](https://en.wikipedia.org/wiki/ARM_architecture_family#Cores)
- [GCC x86\_64 Compiler Options](https://gcc.gnu.org/onlinedocs/gcc/x86-Options.html#index-march-16)
- [GCC aarch64 Compiler Options](https://gcc.gnu.org/onlinedocs/gcc/AArch64-Options.html#index-march)

## x86-64-v4

This is our default and most widely available Microarchitecture (formally named
`avx512`) and includes Intel Cascade Lake-SP, Ice Lake-SP, Sapphire Rapids-SP, Emerald Rapids-SP, and AMD
Zen4 CPUs. There are no special requirements for running on this architecture and most
software should work by default.

## x86-64-v3

This Microarchitecture was formally named `avx2` and includes Intel Haswell, Broadwell, and AMD Zen3 CPUs. 


## neoverse-v2

This Microarchitecture includes NVIDIA Grace Hopper (ARMv9.0-A). Slurm specific
notes for running on this architecture:

- When running `sbatch` or `srun` you need to set `--export=HOME,TERM,SHELL`
- Interactive job submission via `salloc` requires `--no-shell`  
- Ensure all your sbatch scripts have this at the top: `#!/bin/bash -l`  
- Make sure you're NOT pinning any ccrsoft release in `~/.modulerc`  
- Make sure to release the node when done using the `scancel` command  

Example of submitting an interactive job on the Grace Hopper nodes:

```
$ salloc \
   --partition=arm64 \
   --qos=arm64 \
   --mem=45G \
   --nodes=1 \
   --time=1:00:00 \
   --ntasks-per-node=1 \
   --cpus-per-task=32 \
   --gpus-per-node=1 \
   --constraint=GH200 \
   --no-shell
# above command will output jobid
$ srun --jobid=JOBID_HERE --export=HOME,TERM,SHELL --pty /bin/bash --login
```  
Once you're done with the node, use the `exit` or `logout` command and then release your job using the command:  
`scancel {JOBID}`

Example of an sbatch script for running on the Grace Hopper nodes:

```bash
#!/bin/bash -l

#SBATCH --partition=arm64
#SBATCH --qos=arm64
#SBATCH --time=00:40:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=64
#SBATCH --mem=64G
#SBATCH --gpus-per-node=1
#SBATCH --export=HOME,TERM,SHELL
#SBATCH --constraint=GH200
#SBATCH --output=results.txt
```

These are simple examples.  For more information on properly requesting cores and nodes, [see here](../hpc/jobs.md#requesting-cores-and-nodes).  For more details on Slurm directives [see here](../hpc/jobs.md#slurm-directives-partitions-qos).  

For GPU workloads we highly recommend using [NVIDIA NGC containers](https://catalog.ngc.nvidia.com/containers). For example, here's NGC
[TensorFlow](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/tensorflow)
and [PyTorch](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch).
For an example of how to run an NGC container using slurm see our example
sbatch script here: `/util/software/examples/gracehopper/slurm-job.sh`
