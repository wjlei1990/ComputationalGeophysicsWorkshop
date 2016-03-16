## How to run SPECFEM3D_GLOBE
This is a simple instruction about how to quickly run the SPECFEM3D_GLOBE.

#### 1. Obtain the code:

1. google search `specfem3d globe` and you will find this link: https://geodynamics.org/cig/software/specfem3d_globe/. It has instructions about how to "download" the code:
  ```
  git clone --recursive --branch devel https://github.com/geodynamics/specfem3d_globe.git/
  ```

2. For this workshop, you shall git clone from my local repo:
  ```
  cd ~; git clone /scratch/fast/lei/specfem3d_globe
  ```

#### 2. Checkout out what is inside the package, for example, see what is inside in the following directories:
  * DATA
  * src

#### 3. Prepare the input file
  * `DATA/CMTSOLUTION`
  * `DATA/STATIONS`
  * `DATA/Par_file`

#### 4. Compile the code
  1. configure to generate make file
  2. compile the code using `Makefile`

See what has been generated inside `bin`

#### 5. Generate the mesh using internal mesher

#### 6. Launch the simulation.
