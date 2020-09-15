# Numerical Simulation of a Laminar Flow past a Circular Cylinder at Reynolds Number = 100, using OpenFOAM v7 
The simulation is a part of our Undergraduate Project titled **'Rough Walls'** conducted in the school of Mechanical Sciences at Indian Institute of Technology Goa.
- Authors: Tushya Chheda, Jainam Jain, Y. Sudhakar
- E-mail: {tushya.chheda.18003, jainam.jain.18003, sudhakar}@iitgoa.ac.in

The simulations are performed with OpenFOAM v7 in serial and in parallel modes using a machine running Ubuntu 20.04.

## Fundamental Information
- Inlet Velocity, Ux = 1m/s
- Diameter of the circular cylinder, D = 1m
- Reynolds Number, Re = 100
- Kinematic Viscosity, v = 0.01m<sup>2</sup>/s

## Domain Specifications
A Rectangular Domain with length = 33m, height = 16m, width = 1m and the bounding coordinates (-8 -8 -0.5) (25 8 0.5), is used to perform the simulations. The  circular cylinder of diameter(D) = 1m, is fixed with the center at origin (0 0 0), where D is taken to be the characteristic length here. It can be seen in the image that the domain stretches for 25 characteristic lengths to the right (25D = 25m), 8 characteristic lengths to the left (8D = 8m), 8 characteristic lengths to the top (8D = 8m) and 8 characteristic lengths to the bottom (8D = 8m) with respect to the center of the cylinder.

In order to capture the Solution i.e. Drag & Lift Coefficients at the cylinder surface and Vortex Shedding Phenomena in the wake, we need a finer mesh near the cylinder & the wake region of the cylinder respectively and coarser mesh at the boundary of the rectangular domain. A graded structured mesh is formed using blockMesh to achieve the required meshing.
- Number of Mesh Points Generated (nPoints) = 94,186
- Number of Mesh Cells Generated (nCells) = 46,630

The image shows the close-up view of the mesh around the cylinder and wake region.

## Boundary Conditions
Velocity Boundary Conditions: 
- A fixed uniform inlet velocity, Ux = 1m/s Uy = 0m/s Uz = 0m/s is given at the inlet patch.
- Neumann Boundary Condtion is applied with zeroGradient at the oulet patch.
Pressure Boundary Conditions:
- Neumann Boundary Condtion is applied with zeroGradient at the inlet patch.
- A fixed uniform 0 pressure condition is given at the outlet patch.
Top and Bottom patches are given a symmetry condition using symmetryPlane.
Cylinder surface is given no-slip condition.
Front and Back patches are kept empty i.e. devoid of boundary conditions.

## Running The Simulation
To Generate Mesh:
>$ blockMesh

To Check Mesh Quality:
>$ checkMesh

To Run the Simulation 
- in Series:
    >$ icoFoam
- in Parallel: 
    We need to first Decompose the Mesh, edit the file *system/decomposeParDict* by running the following command:
    >$ decomposePar
    
    As the number of subDivisions mentioned in the casefile is 4 and further it's mentioned how many divisions in respective directions, so the mesh will get     divided into 4 divisions, 2 in x directions and 2 in y directions; the mesh will be allocated to 4 processors of the system.
    >$ mpirun -np 4 icoFoam -parallel > log &
    
    Before viewing the results we need to Reconstruct the mesh by running:
    >$ reconstructPar
    
    After reconstructing we need to kill the processors which were allocated to the 4 sub-divisions of the mesh by the following command:
    >$ rm -rf processor*
    
## Post-Processing:
Post Processing is done using paraview which can be done in two ways:
- Method 1:
    >$ paraFoam &
    
- Method 2:
    - Firstly we need to convert the files in the format as identified by Paraview by running the command:
        >$ foamToVTK
        
    - After running the previous command, a directory named VTK is created which has the directories at different intervals of time which further contains a file named internal.vtu which is identified by Paraview.
    - Paraview is launched and internal.vtu is opened and all the data is further extracted from there.
- Also the Lift & Drag Coefficients are found in *postProcessing/forces/0* directory.
