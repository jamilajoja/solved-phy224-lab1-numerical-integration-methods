Download Link: https://assignmentchef.com/product/solved-phy224-lab1-numerical-integration-methods
<br>
Numerical integration methods

<h1>The spring and mass</h1>

You will get experimental data of a mass-spring system, and write a Python program to solve the equation of motion. You will then use this simulation data to plot a visualization of position vs. time and the phase plot. You will also calculate the energy and plot it. You will have to discuss the output, and eventually improve the code.

This lab contains explicit questions for you to answer labelled with <strong>Q</strong>. However, you still need to maintain a notebook for the lab, make plots and write Python code.

<h1>Background knowledge for exercise 5</h1>

<strong>Python </strong>lists, arrays, numpy, pyplot

<strong>Physics </strong>Harmonic oscillator, Hooke’s law. Review these from your first year text.

<h1>1           First Session</h1>

<h2>1.1         Introduction</h2>

Physics of springs is based on Hooke’s Law

<em>F</em><sub>spring </sub>= −<em>ky ,                                                     </em>(1)

where <em>y </em>is the vertical displacement, and <em>k </em>is the spring constant measured in N/m. Hooke’s law can be used with Newton’s second law to derive the equation of motion:

d<sup>2</sup><em>y        k</em>

+        <em>y </em>= 0<em>.                                                  </em>(2)

d<em>t</em><sup>2           </sup><em>m</em>

<strong>Q1 </strong>Show how equation (2) was derived. Point out the main approximations involved (if any).

The most common method used to find numerical solutions to equations of motion is by setting up a pair of <em>coupled ordinary differential equations</em>.

Given a mass, <em>m</em>, coordinate <em>~q</em>, momentum <em>p~</em>, and force <em>F~</em>,

(3a)

d<em>~q     p~                                                                        </em>Figure 1: A vertical spring-mass

= <em>.        </em>(3b) system d<em>t m</em>

<strong>The force can be any function of </strong><em>p~ </em><strong>and </strong><em>~q </em><strong>in general, but in this exercise, we will look at a linear spring: </strong><em>F</em><em><sup>~</sup> </em>= <em>F</em><em><sup>~</sup></em><sub>spring</sub>

<h2>1.2         Numerical Methods</h2>

The solution to equation (2) is well-known, but in general, differential equations can be difficult to solve. In practice, we can calculate approximate solutions by approximating the derivatives as

d

<em>                                   .                                                                       </em>(4)

d<em>t        </em>∆<em>t</em>

Therefore, equations (3) can be approximated with

))                                                                    (5a)

(5b)

Equations (5) are <em>update formulae</em>. Given initial position, momentum, and starting time <em>t </em>= <em>t</em><sub>0</sub>, we can determine a numerical approximation of position and momentum at times <em>t</em><sub>0 </sub>+ ∆<em>t,</em>2∆<em>t,…</em>. The numerical solution will approach the actual solution as ∆<em>t </em>→ 0.

This time-stepping scheme is called the “Forward Euler” method, because it uses the derivative at the start of an interval to extrapolate <em>forward</em>. We will see other time-stepping schemes in the next session. The scheme can also be written in a recursive form,

<em>p~<sub>i</sub></em><sub>+1 </sub>= <em>p~<sub>i </sub></em>+ ∆<em>tF</em>(<em>~q<sub>i</sub></em>)                                                                              (6a)

(6b)

where <em>p~<sub>i </sub></em>= <em>p~</em>(<em>t<sub>i</sub></em>), <em>~q<sub>i </sub></em>= <em>~q</em>(<em>t<sub>i</sub></em>), and <em>t<sub>i </sub></em>= <em>t</em><sub>0 </sub>+ <em>i</em>∆<em>t</em>.

<h2>1.3         Numerical methods for the mass-spring system</h2>

The equation of motion for the vertical spring-mass system can be written in the coupled form as:

d<em>v      </em>−Ω2<sub>0</sub><em>y                                                                                     </em>(7a)

=

d<em>t</em>

d<em>y</em>

= <em>v ,                                                                                            </em>(7b)

d<em>t</em>

where Ω<sub>0 </sub>= <sup>p</sup><em>k/m </em>is the angular frequency of oscillation.

The initial conditions will be <em>y</em><sub>0 </sub>= <em>A </em>(the amplitude measured in experiment), and <em>v</em><sub>0 </sub>= 0 m/s. Using (7), the numerical approximation can be written as

<table width="369">

 <tbody>

  <tr>

   <td width="345"><em>y</em><em>i</em>+1 = <em>y</em><em>i </em>+ ∆<em>tv</em><em>i</em></td>

   <td width="24">(8a)</td>

  </tr>

  <tr>

   <td width="345"></td>

   <td width="24">(8b)</td>

  </tr>

 </tbody>

</table>

for <em>i </em>= 0<em>,</em>1<em>,</em>2<em>,…</em>. This is the update scheme you will use in your first program.

<strong>Q2 </strong>Show the derivation of equations (8) using the equation of motion (2) and the definition of the Forward Euler method (5).

<h2>1.4         The experiment</h2>

You should have a mass hanging from a spring. Underneath the mass is a motion sensor, which is plugged into a data acquisition device (DAQ). The output of the DAQ is analyzed by a LabView application

(~Desktop2nd Year lab FilesMotionSensor.vi)

The goal of the lab exercise is to determing the period of oscillation of the bob, <em>T </em>(and therefore the frequency Ω<sub>0</sub>). This will be used in our later analysis. Do the following:

<ol>

 <li>Measure the mass of the bob.</li>

 <li>Open vi.</li>

 <li>Switch to the “Setup/Callibrate” panel, and change the samples/second to 100.</li>

 <li>Switch to the “Collect” panel. Position the bob at about 20 cm above the motion sensor.</li>

 <li>Start the bob oscillation by either raising or lowering it from equilibrium and letting go; a few centimeters should be enough.</li>

 <li>Click “start detector” the motion sensor should start buzzing now. Click “Collect Data” to begin the data collection.</li>

 <li>Let the bob oscillate for about 10 seconds, then stop the detector.</li>

 <li><em>If the motion sensor is not aligned well, the data may be poor. As long as the graph shows a fairly regular motion, it should be possible to measure the period.</em></li>

 <li>Switch to the “Analyze” panel. Adjust the yellow cursors to the begining and end of 5 to 10 oscillations.</li>

 <li><em>You may need to change the bounds of the plot to get a closer view. You do this by highlighting the last value on either scale and replacing it by your value.</em></li>

 <li>Read the time between cursors, and divide by the number of oscillations observed to get the period.</li>

 <li>Record the period.</li>

 <li>Open File/Position Data Set. Save the data file on your memory stick.</li>

 <li>Plot Distance vs. Time with labelled axes. <em>Ignore the ”Dist. Error” for now.</em>. Calculate the period from your plot.</li>

</ol>

<strong>Q3 </strong>What is the value of the spring constant, <em>k</em>?

<h2>1.5         Python programming</h2>

Scripts for simulations typically follow the same pattern

<ol>

 <li>define constants/parameters</li>

 <li>set the initial conditions</li>

 <li>use the numerical approximation (8) to step forward in time</li>

 <li>loop until the final time</li>

 <li>plot the graph and interpret the result</li>

</ol>

Additional steps that may be useful include

<ul>

 <li>wrapping it in a function for repeated simulations,</li>

 <li>saving the data for later analysis.</li>

</ul>

The outline for our specific program is,

<ol>

 <li>import required modules (eg. pylab, or numpy and matplotlib.pyplot) 2. define constants ∆<em>t </em>and Ω<sub>0</sub>.</li>

 <li>calculate the time values, <em>t<sub>i </sub></em>for the plot using ∆<em>t </em>= 0<em>.</em>01 s, <em>t</em><sub>0 </sub>= 0 s, <em>T </em>= 10<em>.</em>0 s.</li>

 <li>preallocate the array (with the zeros() function)</li>

 <li>set initial conditions</li>

 <li>write the time-stepping loop</li>

 <li>plot the data (<em>position vs. time</em>) with labelled axes</li>

</ol>

Write and run the program. Save the program and its output on your memory stick.

<h2>1.6         Programming – Analysis</h2>

<strong>Q4 </strong>What do you see happening in the plot? Is this what you expect? Can you interpret the graph?

There are other graphs that are useful for analysis:

<ol>

 <li>‘velocity vs. time’ (time on horizontal axis, velocity on vertical axis)</li>

 <li>‘velocity vs. position’ (position on horizontal axis, velocity on vertical axis)</li>

</ol>

The latter is called a phase-plot.

Create these plots with labelled axes and save them.

<h3>1.6.1         Energy</h3>

Energy (and other conserved quantities) are very useful for analyzing dynamical systems. For the spring-mass system, the mechanical energy is conserved,

<em>E</em><sub>tot </sub>= <em>K</em>(<em>y</em>˙) + <em>U</em>(<em>y</em>)<em>,                                                                                  </em>(9)

where <em>K </em>is kinetic energy () and U is potential energy (both elastic and gravitational). The energy expression we will use is

<em> .                                                                           </em>(10)

The term for gavitational potential energy can be omitted by wisely choosing the reference for potential energy. <em>You should be able to prove this statement</em>.

<ul>

 <li>Modify your program to calculate the energy at each step. Note that the energy is not zero at <em>t </em>= 0. The mass (<em>m</em>) and spring constant (<em>k</em>) will need to be added to your code.</li>

 <li>Plot ‘Energy vs. time’</li>

</ul>

<strong>Q5 </strong>What does the energy plot suggest? Does this explain the strange appearance of the <em>velocity vs. time </em>and <em>velocity vs. position </em>plots?

<strong>Q6 </strong>For a spring-mass system, the phase plot should be an ellipse. Explain why, using energy conservation. Give an explanation for the appearance of your phase plot.

<strong>Q7 </strong>(bonus) Determine the leading error in our numerical method. Hint: use a Taylor expansion of <em>y</em>(<em>t</em>+∆<em>t</em>) and find the terms we ignored in equation (5).

<h2>1.7         More on numerical integration schemes</h2>

If you properly implemented the numerical approximation in Equation (8), you should have found that the simulation was bad: the amplitude increased, and energy was not conserved. The reason for the failure was the integration method. We will discuss other numerical integrators, and implement a symplectic scheme, which is suitable for conservative systems.

In the first program, we used the most primitive numerical integration method called the <em>Forward Euler </em>or <em>Explicit Euler </em>method,

<em>y</em>[<em>i </em>+ 1] = <em>y</em>[<em>i</em>] + ∆<em>tv</em>[<em>i</em>] <em>v</em>[<em>i </em>+ 1] = <em>v</em>[<em>i</em>] − ∆<em>t</em>Ω<sup>2</sup><sub>0</sub><em>y</em>[<em>i</em>]<em>.</em>

Forward Euler extrapolates the position through an interval ∆<em>t </em>using only the (approximate) derivative at the begining of the interval. <em>It can be proved [</em><em>1] that Forward Euler is unstable, which means that the amplitude and total energy increases in time</em>. In phase space, the increase in energy looks like a spiral outward. <strong>The accuracy of the Forward Euler method can be improved by decreasing the time step, but the energy will always increase.</strong>

A similar method to Forward Euler is <em>Backward Euler </em>or <em>Implicit Euler</em>. This method uses the derivative at the end of the interval (making an implicit scheme) to calculate the next point,

<table width="400">

 <tbody>

  <tr>

   <td width="369"><em>y</em>[<em>i </em>+ 1] = <em>y</em>[<em>i</em>] + ∆<em>tv</em>[<em>i </em>+ 1]</td>

   <td width="31">(11a)</td>

  </tr>

  <tr>

   <td width="369"><em>v</em>[<em>i </em>+ 1] = <em>v</em>[<em>i</em>] − ∆<em>t</em>Ω<sup>2</sup><em>y</em>[<em>i </em>+ 1]<em>.</em></td>

   <td width="31">(11b)</td>

  </tr>

 </tbody>

</table>

Backward Euler is absolutely stable, which means that longer timesteps can be used (especially for “stiff” or rapidly changing ODEs). However, it <em>artificially dissipates </em>energy.

A simple remedy is to combine the Forward and Backward Euler methods to create the <em>Euler-Cromer </em>or <em>Symplectic Euler Method</em>,

]                                                                               (12a)

<em>.                                                                 </em>(12b)

The result is an explicit method, which <em>conserves </em>approximate energy. Do the following:

<ul>

 <li>Insert the new code lines for the symplectic method (12) into your previous program, and plot the “Energy vs. time” and phase plots.</li>

</ul>

You may want to simulate using both methods, and plot both results on the same axes.

<ul>

 <li>Compare and discuss the plots from the Forward Euler and Symplectic Euler Methods. Use the same time step for both methods in the comparison.</li>

</ul>

<strong>Q8 </strong>How do the energy and phase plots change using the symplectic method?

<strong>Keep in mind for the future that it is essential to use a method that conserves energy (e.g. symplectic methods) when simulating conservative problems.</strong>

<h3>Your submission for this exercise should include</h3>

<ul>

 <li>All plots marked above (position, energy, and phase space plots for both Forward and Symplectic Euler Methods)</li>

 <li>answers to questions 1-8,</li>

 <li>the final version of your program,</li>

 <li>values from your experiment (period, amplitude, frequency, and spring constant).</li>

</ul>

<h1>2           Second session</h1>

In the first part of this exercise, we analyzed the equation of motion of a spring-mass system and wrote Python code to numerically integrate the equation. In this session, we will add a physical damping term, and <em>qualitatively </em>compare the numerical simulation to the experiment.

<h2>2.1         Adding a damping term</h2>

In the real world, mechanical energy cannot be perfectly conserved. So far, the equations of motion you have used model the system <em>without damping </em>(physical dissipation). In general, the damping force exerted on a body depends on the velocity <em>~v </em>of the body. Drag is one source of damping caused by velocity of a body relative to the surrounding medium (air or water) commonly modelled as quadratic drag,

(13)

where

<em>C </em>is the drag coefficient (dimensionless), <em>ρ </em>is the density of the medium (kg/m<sup>3</sup>),

<em>A </em>is the cross-sectional area perpendicular to the flow (m<sup>2</sup>), and <em>~v </em>is the velocity of the body relative to the medium (m/s).

The direction of the damping force is always opposite to the direction of velocity. The drag coefficient is not a universal constant: it depends on viscosity of the medium, shape of the body, and roughness of its surface. It also depends on the velocity through the Reynolds number.

The <em>Reynolds number </em>Re, is a very useful dimensionless quantity used to characterize flows in fluid mechanics. In our case, it will characterize the dependence of the drag coefficient on velocity. The Reynolds number is the ratio of the inertial force of the medium to the viscous force:

Re =                                                                                        (14)

where

<em>ρ </em>is the density of the medium (kg/m<sup>3</sup>), <em>v </em>is the velocity of the body relative to the medium (m/s), <em>l </em>is the characteristic length in the direction of flow (m), and <em>η </em>is the dynamic viscosity (N·s/m<sup>2</sup>).

If the flow is <em>laminar</em>, the Reynolds number takes small values (Re <em>&lt; </em>2300) and the drag coefficient is inversely proportional to the velocity. This makes the drag force directly proportional to velocity:

(15)

where <em>γ </em>is the damping coefficient.

When the flow is turbulent, the Reynolds number is large (Re <em>&gt; </em>4000) the drag coefficient is approximately constant and the drag force is dependent on the square of the velocity.

<strong>Q9 </strong>What is the Reynolds number for the spring-mass system? <em>Hint: this may depend on the amplitude of the oscillation.</em>

We expect that the motion and speed of a typical mass-spring system in air correspond to small Reynolds numbers. Therefore, the equation of motion of our system would be written as:

d

<em>                                   .                                                                          </em>(16)

d<em>t</em>

<strong>Q10 </strong>Using the above equations, estimate the damping coefficient <em>γ</em>. You’ll do it experimentally in the next section.

<h2>2.2         Repeat the experiment</h2>

The effects of damping were likely not seen in the last session, because the damping for the bob is quite small. To make damping more observable, we can attach a disk to the bob to increase drag.

<ul>

 <li>Attach the damping disk to the bob.Weigh the new system.</li>

 <li>Repeat the experiment as outlined in Section 4 for a longer period of time so that you can see the decay – about 2 minutes with the fin attached. <strong>Note: because the experiment setup has changed, you should measure the frequency and mass again this session.</strong></li>

 <li>Using the cursors, take 5-6 readings of amplitude. Assuming an exponential decay of the oscillation envelope, estimate the decay constant <em>γ </em>(<em>γ/</em>2 is the inverse of time for which amplitude falls to 1<em>/e </em>of the initial value). <em>You do not have to use Python to do this calculation. Please verify that the exponent in position decay is γ/</em>2 <em>while the exponent in energy decay is γ.</em></li>

 <li>Save the position vs. time plot.</li>

 <li>Export the data in case you need it later.</li>

</ul>

<h2>2.3         The new Python program</h2>

The coupled equations we need to formulate for our new Python program are

<sup>d<em>v </em></sup>= −Ω<sup>2</sup><sub>0</sub><em>y </em>− <em>γv            </em>(17a) d<em>t</em>

d<em>y</em>

= <em>v                                                                                                 </em>(17b)

d<em>t</em>

Modify your program from part 1.3 to include drag with (17) and plot ‘Position vs. time’ and ‘energy vs. time’. Use the decay coefficient determined experimentally.

<strong>Q11 </strong>Discuss the plot. What effect does damping has on the energy?

<h2>2.4         Compare with experimental data</h2>

The practice of Physics often includes these steps:

<ul>

 <li>come up with a (mathematical) model for a phenomenon,</li>

 <li>make predictions with that model,</li>

 <li>compare those predictions against experiment.</li>

</ul>

The comparisons can be qualitative (e.g. do both the predicted and measured amplitudes decay with time?), or quantitative (e.g. what is the difference in period between the prediction and experiment?). For now, we will just do a qualitative comparison. Fitting this complex function with curve_fit is very hard and requires a carefully designed fitting routine to find the correct answer.

<strong>Q12 </strong>Compare the experimental data with the output of your program. What do you think makes them different?

Your submission for this exercise should include:

<ul>

 <li>plots for position and energy of the damped system,</li>

 <li>a plot of the experimental data,</li>

 <li>answers to questions 9-12,</li>

 <li>the final version of your program,</li>

 <li>values from your experiment (period, frequency, decay rate, and spring constant).</li>

</ul>

<h1>References</h1>

[1] William H Press, Saul A Teukolsky, William T Vetterling, and Brian P Flannery. <em>Numerical recipes in C</em>, volume 2. Cambridge university press Cambridge, 1996.

<em>Prepared by John Ladan and Ruxandra Serbanescu, 2016. Edited by Christopher Lee, 2017.</em>