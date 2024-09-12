

SCIF20002 – Programming and Data Analysis for Scientists – Final Assessment


Scientiﬁc problems from the gravitational dynamics of planets to the motion of atoms in a gas require us to be able to compute the behaviour of many interacting bodies.  One common approach is to perform a so-called N-body simulation. In an N-body simulation we track the positions and velocities of individual particles,  and use the forces between them to calculate their individual accelerations.
For this assessment, you will write an N-body code to simulate the behaviour of argon atoms conﬁned within  a box.   You will then use this code to investigate how the pressure inside the box changes as you alter the system parameters.   You will then write up your work,  detailing how you set-up your code, demonstrating that it performs as expected for any relevant test cases, and showing your results.  Your report should conclude with a discussion of any deﬁciencies and possible improvements that could be made.
You may use either C++ and/or Python as you see ﬁt, but your report must justify the choice. You are welcome to use any code that you have produced during this course (including example code we have provided) but it must be properly attributed.

Part 1 – Producing the N-body code
An N-body code must follow the trajectories of a ﬁxed number of particles,  N.  Each particle, i i i  vector in 3D space.  Particles interact with one
another via the force between them. If the force on particle i due to particle j is given by ij , we
can ﬁnd the net force acting on particle i by summing over all particles (except for i!), i.e.

The acceleration of particle i, a→i  then follows from Newton’s second law as

where mi  is the mass of particle i.  From the acceleration, we can then calculate the velocity and position and how they change over a given time-step, δt. As will be clear shortly we will consider interactions between particles where the force they exert depends only on their relative positions.

To perform the integration, we use a so-called Verlet ‘leap-frog’ integration scheme.  For each particle i, we update the velocity based on the acceleration at the current time-step using half the step size

This must be done for all the particles in our simulation. We then use these new velocity to update the position across the whole time interval
r→i  = r→i + δtv→i.
Again, this must be done for all the particles.  Finally, we use the new positions to recompute the acceleration a→i  (this is why we had to update the positions of all the particles ﬁrst!)  and then calculate the new velocity after the remaining half time step:

To model the interaction between two atoms in a gas we will use the Lennard-Jones potential

where r =   parameters that depend on the atoms.  For argon, E = 125.7 × kB  and σ = 0.3345 × 10-9 m.  Given this radially symmetric interaction potential, an atom j exerts a force on atom p as

where
ji  =                                                                      (3)
is a unit vector pointing from atom i to atom j.
Task:  Create a piece of code that can perform the Verlet integration described above for a system of N particles. Demonstrate that the code behaves as expected for a system of two particles in close proximity (i.e.  with a separation of the order of σ).  Place one particle at the origin and the other at a point on the x-axis.  Show that the two particles can remain bound to one another, and that they oscillate in place.  Your report should include a brief description of your code, and plots to demonstrate the required behaviour.
It is advisable you use a dimensionless formulation of the problem using the fact that the system depends only on the parameters ma , σ and E. We can then deﬁne dimensionless units as
    and                                               (4)
where we ﬁx the time scale τ from E as
                                                                      (5)

Having done this all energies are measured relative to E, all speeds are measured relative to σ/τ = √E/ma , and accelerations are relative to σ/τ 2  = E/ma σ . Consequently, Eq. (1) reduces to

while Eq. (2) reduces to

so the equation of motion become
                                              (8)
Thus, in our chosen system of units there is no explicit reference to any of the parameters ma , σ and E. What are the characteristic timescale (τ) and speed (σ/τ) associated with a gas of argon atoms?
You are strongly recommended to consider the e伍ciency of the code!  Use array operations rather than for loops where possible – they are much, much faster!

Part 2 – Particles in a box
We now require some boundary conditions for the simulation.  Assume our particles are going to be conﬁned to a cubic box whose sides have a length of L.  We will assume that the centre of the box is centred on the origin.  Consider a particle travelling only in the x-direction.  When it reaches the wall of the box at x = L/2, it rebounds elastically – i.e. its velocity in the x-direction is reversed, but its speed (and thus its kinetic energy is unchanged).
Task: Add a cubic box to your simulation so that all particles are conﬁned within -L/2 ≤ xL/2, -L/2 ≤ yL/2 and -L/2 ≤ zL/2. Describe how you have implemented the particle-wall collision in your report. Show that a particle hitting the walls of the box behaves as expected by including an appropriate plot.

Part 3 – Investigate!
You now have all the components you need to investigate the behaviour of the gas. The temperature of the gas is deﬁned by the total kinetic energy of the particles as

where vi is the speed of the ith particle. The pressure P is linked to the momentum 且owing through a unit area in a unit time period (note you only need to consider particles passing in one direction through the area). Suppose we have an area, A, lying in the y - z plane. The momentum crossing this plane in time △t is the x-component of the momentum of any particle crossing this plane,

px  = mvx  where vx  is the speed of the particle in the x-direction. The pressure in the x-direction is therefore

where the sum is performed only over those particles i crossing the plane in the time-interval △t. If we assume the pressure is isotropic, Px   = Py   = Pz    might like to test if this is true in your simulations!). Note you also only need to consider particles travelling in one direction, as pressure should be the same in both positive and negative directions when the system is in equilibrium.
Task:  How does the pressure of the gas change with changes in the volume of the box and the temperature of the gas? You will need to calculate the pressure of your gas and its temperature. It is up to you to decide on how many particles N to use, what time-step δt to use, how long to run the simulations for, and what initial conditions you use.  Your choices should be justiﬁed in your report based on valid scientiﬁc/computational reasons.
Hint:  It is strongly recommended that you initialize the positions of your particles on a grid whose spacing is no smaller than the value of σ . The steep dependence of the potential for small r can lead to extremely large forces if you initialize the particles too close to one another. Also, the temperature and pressure estimated from your simulations will be very stochastic on the micro- scopic time-scales you will examine.  Consider performing time-averaging to extract the expected behaviour.
Submisssion
Your submission must consist of both your (documented) code and a report into your investigation of how the gas behaves. You must include working examples for the ﬁrst two tasks which we must be able to run. It should be clear how these test cases are linked to the code you use in the ﬁnal investigation of the gas. Your report should include details of how you tested your code to ensure that it is working as intended (e.g.  does the code conserve energy su伍ciently well?), how many particles you chose to use and the length of time you chose to run your simulations for.
Please submit your report as a PDF document via the submission point on Blackboard, along with a ﬁle containing your code and everything needed to run it.
