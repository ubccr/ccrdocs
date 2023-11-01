# Python

Several python modules are available for use. We encourage users to checkout
these modules as they include lots of common scientific python packages.

| module       | Included python packages                                                                     |
| ------------ | -------------------------------------------------------------------------------------------- |
| python-bare  | Bare python3 interpreter only                                                                |
| python       | Bare python3 plus many common modules                                                        |
| scipy-bundle | beniget, Bottleneck, deap, gast, mpi4py, mpmath, numexpr, numpy, pandas, ply, pythran, scipy |
| tensorflow   | TensorFlow                                                                                   |
| pytorch      | PyTorch                                                                                      |

If you require other specific python modules, we recomend you ask CCR to build
them or create your own python module bundles with easybuild.

Here's an example easybuild recipe the builds a python module from pip:

```python
easyblock = 'PythonBundle'

name = 'mygroup-bundle'
version = '1.0.0'

homepage = 'https://github.com/ubccr/software-layer'
description = """
Custom python modules for my group
"""

toolchain = {'name': 'foss', 'version': '2021b'}

# list any other dependencies here
dependencies = [
    ('Python', '3.9.6'),
    ('SciPy-bundle', '2021.10'),
]

exts_list = [
    # sha256 checksum can be found on pypi, for example:
    # https://pypi.org/project/fuzzywuzzy/#copy-hash-modal-bdeeeb75-5450-499a-ae89-21c91611d2c7
    ('fuzzywuzzy', '0.18.0', {
        'checksums': ['45016e92264780e58972dca1b3d939ac864b78437422beecebb3095f8efd00e8'],
    }),
]

sanity_pip_check = True
use_pip = True

moduleclass = 'math'
```

Save the above to a file called `mygroup-bundle-1.0.0-foss-2021b.eb`. To install run:

```
$ module load easybuild
$ export CCR_BUILD_PREFIX=/projects/academic/grp-ccrstaff/easybuild
$ eb mygroup-bundle-1.0.0-foss-2021b.eb
```

To use run:

```
$ module load mygroup-bundle
$ python3
$ import fuzzywuzzy
```
