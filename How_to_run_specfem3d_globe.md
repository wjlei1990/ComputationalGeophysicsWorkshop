## How to run SPECFEM3D_GLOBE
This is a simple instruction about how to quickly run the SPECFEM3D_GLOBE.

#### 1. Obtain the code:

1. google search `specfem3d globe` and you will find this link: https://geodynamics.org/cig/software/specfem3d_globe/. It has instructions about how to "download" the code:
  ```
  git clone --recursive --branch devel https://github.com/geodynamics/specfem3d_globe.git/
  ```

2. **For this workshop**, you shall git clone from my local repo. First, log into mcmillan with you account and type the command in the terminal:
  ```
  cd ~; git clone /scratch/fast/lei/specfem3d_globe; cd specfem3d_globe
  ```

#### 2. Checkout out what is inside the package, for example, see what is inside in the following directories:
  * `DATA`: `CMTSOLUTION`, `STATIONS`, `Par_file`
  * `src`: just a quick look

#### 3. Prepare the input file
  * `DATA/CMTSOLUTION`
    replace with the earthquake source you want. Format should follow: http://www.globalcmt.org/CMTsearch.html. Also documented in the manual, page 27.
  * `DATA/STATIONS`
    replace with you station distribution. Details in the manual, page 29. 
  * `DATA/Par_file`
    This part requires special attention, I will guide you through the `Par_file`.

#### 4. Compile the code
  1. check out your system environment and load necessary modules.
    Sine specfem runs in parallel and thus you need to compile the package with parallel compiler.
    Suppose you are going to use gnu compiler on mcmillan, type this in the terminal:
    ```
    module load openmpi/gcc
    ```
    
    Then type in this terminal to check the C and Fortran compiler: `mpicc --version` and then `mpif90 --version`. I assume you won't see any error messages
  1. configure to generate make file. In terminal:
    ```
    ./configure FC=mpif90 CC=mpicc
    ```
    This will generate the `Makefile`.
    
  2. compile the code using `Makefile`. In terminal:
    ```
    make
    ```
  See what has been generated inside directory `bin`.

---

#### 5. Generate the mesh using internal mesher.
We are going to use the excutable: `bin/xmeshfem3D`, which is an internal mesher embedded in the specfem3d_globe. Then number of processers you are going to use is determined by parameter in the `DATA/Par_file`:
  ```
  Number_of_processors = NPROC_XI * NPROC_ETA * NCHUNKS
  ```

Then you are going to write a job submission script to submit the job to the queue. This script depands on the queue system on your cluster, for example, whether it is `PBS` or `SLURM` systerm. But an example for `SLURM` on mcmillan would be:
```
#!/bin/bash
#SBATCH -N 1 # node count
#SBATCH --ntasks-per-node=6
#SBATCH -t 1:00:00

# Load openmpi environment
module load openmpi/gcc

mpiexec -n 4 ./bin/xmeshfem3D
```
Name this file as "job_mesh.bash" and place it at the specfem3d_globe home directory.

Using `sbatch job_mesh.bash` to submit the job.

#### 6. Launch the simulation.
We are going to use the excutable: `bin/xspecfem3D`. The number of processors you are going to use is the same as the mesher. Then you are going to write a job submission script to submit the job to the queue.
```
#!/bin/bash
#SBATCH -N 1 # node count
#SBATCH --ntasks-per-node=6
#SBATCH -t 1:00:00

# Load openmpi environment
module load openmpi/gcc

mpiexec -n 4 ./bin/xspecfem3D
```

Name this file as `job_solver.bash` and using `sbatch job_solver.bash` to submit the job.
