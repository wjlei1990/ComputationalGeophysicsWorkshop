## How to run SPECFEM3D_GLOBE
This is a simple instruction about how to quickly run the SPECFEM3D_GLOBE.

#### 1. Obtain the code:

1. google search `specfem3d globe` and you will find this link: https://geodynamics.org/cig/software/specfem3d_globe/. It has instructions about how to "download" the code:
  ```
  git clone --recursive --branch devel https://github.com/geodynamics/specfem3d_globe.git/
  ```

2. For this workshop, you shall git clone from my local repo:
  ```
  cd ~; git clone /scratch/fast/lei/specfem3d_globe; cd specfem3d_globe
  ```

#### 2. Checkout out what is inside the package, for example, see what is inside in the following directories:
  * `DATA`
  * `src`

#### 3. Prepare the input file
  * `DATA/CMTSOLUTION`
    replace with the earthquake source you want. Format should follow: http://www.globalcmt.org/CMTsearch.html. Also documented in the manual, page 27.
  * `DATA/STATIONS`
    replace with you station distribution. Details in the manual, page 29. 
  * `DATA/Par_file`
    This part requires special attention, I will guide you through the `Par_file`.

#### 4. Compile the code
  1. check out your system environment and load necessary modules
    Suppose you are going to use gnu compiler on mcmillan:
      ```
      module load openmpi/gcc
      ```
    Then type in this command to check the C and Fortran compiler: `mpicc --version` and then `mpif90 --version`. I assume that you won't see any error messages pops out.
      ```
  1. configure to generate make file
  2. compile the code using `Makefile`

See what has been generated inside `bin`

#### 5. Generate the mesh using internal mesher

#### 6. Launch the simulation.
