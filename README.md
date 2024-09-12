# SCIF20002 – Programming and Data Analysis for Scientists – Final Assessment

## Overview

Scientific problems from the gravitational dynamics of planets to the motion of atoms in a gas require us to compute the behavior of many interacting bodies. One common approach is to perform an N-body simulation. This assessment focuses on simulating the behavior of argon atoms confined within a box, and investigating how the pressure inside the box changes with system parameters.

You are required to write an N-body code, justify your code setup, demonstrate that it performs as expected, and analyze your results. The code must be written in either C++ or Python.

---

## Part 1: Producing the N-body Code

An N-body simulation tracks the positions and velocities of particles, using the forces between them to calculate individual accelerations. The goal is to simulate a system of N particles and compute how their positions and velocities evolve over time. We will:

- Use Verlet 'leap-frog' integration to update the velocity and position of each particle.
- Model interactions between particles using the Lennard-Jones potential.
- Test our code with two particles placed at a distance of the order of the Lennard-Jones parameter `σ`.

### Steps:

1. **Initialize Particles:**
   - Define the number of particles, N, and initialize their positions and velocities.
   
2. **Force Calculation:**
   - Compute forces between particles using the Lennard-Jones potential.

3. **Verlet Integration:**
   - Update the velocity and position using the leap-frog method.

4. **Test Case:**
   - Place two particles, one at the origin and one on the x-axis, and simulate their interaction to check if they remain bound and oscillate.

### Code Outline:

```python
# Initialize parameters such as number of particles, mass, Lennard-Jones potential, etc.

def calculate_force(particle1, particle2):
    # Compute the force between two particles using Lennard-Jones potential
    pass

def verlet_integration(particles, delta_t):
    # Update the velocity and position of particles using Verlet integration
    pass

def simulate(particles, num_steps):
    # Run the simulation for a given number of steps
    pass
