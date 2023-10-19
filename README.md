![Logo Here](pyVisOS.png)

# pyVisOS is a collection of lightweight utilities for manipulating HDF5 files

pyVisOS is designed to be simple to use and easy to understand. The primary goal is to provide an in-memory representation of 
the HDF5 output generated by PIC code OSIRIS. It also provides some functions to automate MPI parallelism.

## The H5Data class for mesh grid quantities
H5Data is a subclass of numpy ndarray with following additional attributes:
* _name_ and _timestamp_: inferred from the filename. These two also serve as default output filename.
* _run_attrs_: a dictionary inferred from the root directory of the HDF5 output. It provides information about the simulation.
* _data_attrs_: a dictionary inferred from the dataset directory. It provides information about the quantity. One quantity for each dataset for the grid type output.
* _axes_: a list inferred from the /AXIS directory. It provides information about the axes. It is always consistent with the data array.

## Function wrappers
A common workflow for data analysis would look like this:

1) load a few quantities into memory
2) distribute the workload across MPI processes
3) data analysis
4) (optionally) gather results from each MPI process and some more analysis (but without redistributing the workload)

Step 3 and 4 are the actual work we should be focusing on and pyVisOS provides a wrapper to automate step 1 and 2 (and partially, step 4).

_independent_timeframe_pptm_: can be used if the analysis can be done in a way that data at different timestamps are independent. see _pynting_flux_example.py_ for details.

**The codes are tested under python 3.5**

## Installation
Pip install the dev branch of this repo directly from github

``pip install git+https://github.com/UCLA-Plasma-Simulation-Group/pyVisOS.git@dev``

Once installed, import any pyVisOS module in python in the normal way:

```
import osh5vis
import osh5io
...
```
