Darshan is a lightweight I/O characterization tool that transparently
captures I/O access pattern information from HPC applications.
Darshan can be used to tune applications for increased scientific
productivity or to gain insight into trends in large-scale computing
systems.

Please see the 
[Darshan web page](http://www.mcs.anl.gov/research/projects/darshan)
for more in-depth news and documentation.

The Darshan source tree is divided into two main parts:

- darshan-runtime: to be installed on systems where you intend to 
  instrument MPI applications.  See darshan-runtime/doc/darshan-runtime.txt
  for installation instructions.

- darshan-util: to be installed on systems where you intend to analyze
  log files produced by darshan-runtime.  See
  darshan-util/doc/darshan-util.txt for installation instructions.

The darshan-test directory contains various test harnesses, benchmarks,
patches, and unsupported utilites that are mainly of interest to Darshan
developers.

# Building Darshan-runtime for Instrumenting Applications on CLAIX-2023

This guide outlines the steps to compile and set up **Darshan-runtime** for instrumenting applications on the **CLAIX-2023** cluster.
## Key Information

- The compiled runtime libraries and binaries will be installed in the following directory:  
  `$HPCWORK/darshan_runtime-claix_2023`.

## Steps to Compile and Install
1. **Prepare the environment**:
    ```bash
    ./prepare
    ```
2. **Navigate to the Darshan-runtime directory**:
    ```bash
    cd darshan-runtime/
    ```
3. **Configure the build**:
    ```bash
    ./configure \
        CC=${MPICC} \
        --with-log-path-by-env=DARSHAN_LOGPATH \
        --with-jobid-env=NONE \
        --with-username-env=SLURM_JOB_USER \
        --enable-hdf5-mod \
        --with-hdf5=/cvmfs/software.hpc.rwth.de/Linux/RH8/x86_64/intel/sapphirerapids/software/HDF5/1.14.0-iimpi-2022a \
        --prefix=$HPCWORK/darshan_runtime-claix_2023
    ```
4. **Build and install**:
    ```bash
    make
    make install
    ```

- Application execution logs generated with Darshan can be saved to the path specified in the `DARSHAN_LOGPATH` environment variable. This path can be defined as needed for your use case.
    
# Building Darshan-utils for Inspecting Darshan Results on CLAIX-2023
## Key Information
- The compiled runtime libraries and binaries will be installed in the following directory:  
  `$HPCWORK/darshan_util-claix_2023`.
  
## Steps to Compile and Install
1. **Navigate to the Darshan-runtime directory**:
    ```bash
    cd darshan-util/
    ```
    
2. **Prepare the environment**:
    ```bash
    ./configure \
      CC=${MPICC} \
      --prefix=$HPCWORK/darshan_util-claix_2023  \
      --enable-pydarshan=yes
    ```

4. **Build and install**:
    ```bash
    make
    make install
    ```

