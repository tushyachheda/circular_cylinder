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
- Number of Mesh Points Generated (nPoints) = 
- Number of Mesh Cells Generated (nCells) = 46,630

The image shows the close-up view of the mesh around the cylinder and wake region.
