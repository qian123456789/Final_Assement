# SCIF20002 – Programming and Data Analysis for Scientists  
## Final Assessment

---

### Introduction
Scientific problems ranging from the gravitational dynamics of planets to the motion of atoms in a gas require us to compute the behavior of many interacting bodies. One common approach is to perform an N-body simulation. In an N-body simulation, we track the positions and velocities of individual particles and use the forces between them to calculate their individual accelerations.

For this assessment, you will write an N-body code to simulate the behavior of argon atoms confined within a box. You will then use this code to investigate how the pressure inside the box changes as you alter the system parameters. Finally, you will write a report detailing your code setup, demonstrating expected test case behavior, and presenting your results. Your report should conclude with a discussion of any deficiencies and possible improvements.

You may use either C++ and/or Python as you see fit, but your report must justify the choice. You are welcome to use any code produced during this course (including provided example code), but it must be properly attributed.

---

### Part 1 – Producing the N-body Code
An N-body code must follow the trajectories of a fixed number of particles \( N \). Each particle \( i \) is a vector in 3D space. Particles interact via the force between them. If the force on particle \( i \) due to particle \( j \) is given by:

$$
\vec{F}_{ij}
$$

The net force acting on particle \( i \) is the sum over all particles (except \( i \)).

The acceleration of particle \( i \) follows Newton’s second law:

$$
\vec{a}_i = \frac{\vec{F}_{ij}}{m_i}
$$

We can then calculate the velocity and position changes over a given time-step \( \delta t \). Interactions between particles are dependent on their relative positions.

We use the Verlet ‘leap-frog’ integration scheme to perform the integration:

1. Update velocity using half the step size:

$$
\vec{v}_i = \vec{v}_i + \frac{\delta t}{2} \vec{a}_i
$$

2. Update position:

$$
\vec{r}_i = \vec{r}_i + \delta t \vec{v}_i
$$

3. Recompute acceleration and update velocity again using the remaining half time-step.

#### Task
Create code for Verlet integration for a system of \( N \) particles. Demonstrate expected behavior for two particles in close proximity. Place one particle at the origin and the other on the x-axis. Include plots showing particles oscillating in place.

You are advised to use dimensionless units:

$$
E = 125.7 \times k_B, \quad \sigma = 0.3345 \times 10^{-9} m
$$

---

### Part 2 – Particles in a Box
We now introduce boundary conditions. Assume particles are confined to a cubic box centered on the origin with side length \( L \). For a particle hitting a wall at \( x = L/2 \), its velocity is reversed, while the speed remains unchanged.

#### Task
Add a cubic box to your simulation and describe particle-wall collision implementation. Include appropriate plots to demonstrate particle behavior upon hitting the walls.

---

### Part 3 – Investigation
The temperature of the gas is defined by the total kinetic energy of the particles:

$$
T = \frac{1}{3k_B N} \sum_i m_i v_i^2
$$

The pressure \( P \) is linked to the momentum crossing a unit area in unit time. For an area \( A \) in the y-z plane, the momentum crossing in time \( \Delta t \) is the x-component of any particle crossing the plane:

$$
P = \frac{1}{A \Delta t} \sum_i m_i v_{ix}
$$

Assume the pressure is isotropic (\( P_x = P_y = P_z \)) and test this in your simulations.

#### Task
Investigate how gas pressure changes with box volume and temperature. Decide on particle number \( N \), time-step \( \delta t \), simulation time, and initial conditions. Justify choices scientifically and computationally.


