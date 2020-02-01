# Saras - Finite-difference solver

Saras is an OpenMP-MPI hybrid parallelized Navier-Stokes equation solver written in C++.
It uses finite-difference methods for spatial discretization along with parallelized algebraic multi-grid method for solving
the pressure correction equation.

All the source and library files for the Saras solver are contained in the following directories:

* ./src/ - contains all the different solvers available in Saras
* ./lib/ - contains all the libraries used by the solvers in ./src/ folder
* ./install/ - contains the installation scripts to build and compile the solver
* ./output/ - the solution files written by the solver are contained in this folder,
            and it is an empty directory as far as Git is concerned since it doesn't track any of the files in it.

## Prerequisites:

* blitz - All array manipulations are done by the blitz library
* cmake - Necessary to make the executable from the source files
* mpich - The compiler used is mpic++
* yaml - The input parameters are stored in the parameters.yaml file which needs the yaml library to parse.
* hdf5 - The output files are written in HDF5 format and requires the HDF5 library

To compile and run the solver, run the compileSaras.sh shell script in the install directory

## Testing SARAS

The Bash shell script testSaras.sh, found in the tests/ folder can be executed to test the solver post-installation.
The script compiles Saras, and runs it with a pre-defined set of parameters.
The parameters file necessary to test the solver with benchmark results of Ghia et al for the lid-driven cavity
(LDC) problem can be found in the input/ folder of tests/ldcTest/.

The test run uses 4 cores and takes about 12 minutes to complete on a desktop workstation.
At the end of the test, the result file output by the solver in the ldcTest/output/ directory is read by a Python script.
The script plots the velocity profiles calculated by Saras and compares the data with the results from Ghia et al.
The following Python modules are necessary for the test to run:

* numpy
* matplotlib
* h5py
* yaml

At the end of the test, the plot is written into a test.png file for the user to verify.


## REFERENCES:

Various articles and pages used to make programming decisions during development of the solver are listed here:

### General stuff

1. http://coding.derkeiler.com/Archive/C_CPP/comp.lang.c/2004-02/1382.html
2. https://stackoverflow.com/questions/4816698/avoiding-circular-dependencies-of-header-files
3. http://blitz.sourceforge.net/resources/blitz-0.9.pdf
4. https://stackoverflow.com/questions/8111677/what-is-argument-dependent-lookup-aka-adl-or-koenig-lookup
5. https://www.codesynthesis.com/~boris/blog/2012/04/04/when-provide-empty-destructor/

### Articles on multi-grid methods

1. http://math.mit.edu/classes/18.086/2006/am63.pdf
2. http://www.mgnet.org/mgnet-tuts.html

### Journal references

1. Ghia, U., Ghia, K. N., & Shin, C. T. (1982). High-Re solutions for incompressible flow using the Navier-Stokes equations and a multigrid method. J. Comput. Phys., 48(3), 387–411. 