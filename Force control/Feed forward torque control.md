# Introduction
 **Force control**
	 Cartesian force control where the end effector can apply a specified force
# Cons of [[PID controller]] in tq ctrl
1.  Gravity biases the torques needed to keep the robot upright. A PID controller compensates for gravity via the integral term, if a joint axis flips orientation, the torque needed is reverse.
2.  The effective inertia of the subchain at each joint is highly dependent on its configuration. For example, if an arm is outstretched, the shoulder joint will need to apply stiffer torques to track a trajectory than if it is tucked.
3.  At high speed, the Coriolis term becomes significant, causing biasing torques that must be compensated.
Conclusion: low flexibility need to tune frequently
# model-based tq ctrl
## Gravity compensation
Dynamics eq: $τ_{ff}=G(q)$, $G(q)$-gravity compensation (GC) $q$ - current
![](http://motion.cs.illinois.edu/RoboticSystems/figures/control/robot_PID_control.svg)
Figure 7. A comparison of piecewise linear and piecewise cubic trajectories executed by PID control or gravity compensation.
	Up: the two trajectories. 
	Down: trajectory tracking errors comparing PID control (PID) against GC for the two types of trajectories. Cubic trajectories demonstrate lower transient error during movement and GC converges more quickly toward zero steady-state error.
GC for $\tau_{ff}$, PID for $\tau_{fb}$  
No load: $τ=τ_{ff}$ (ideally $\tau_{fb}=0$ )
$\tilde{G}(q)$ - GC estimated
With load: $τ=τ_{fb}+τ_{ff}$
## Computed torque control
More than GC, take into account error 

To find $\ddot{q}_D$,
InverseDynamics: $\tau_{ID}(\ddot{q}) = B(q) \ddot{q} + C(q,\dot q) + G(q)$
**Methods**:
1.  feedforward control, combined with a *PID feedback*
	$\tau = \tau_{ID}(\ddot{q}_D) + \tau_{fb}$
2.  computed torque control, *Computed feedback* 
	$\ddot{q}_{fb} = - K_P(q-q_D) - K_I I(t) - K_D(\dot{q}-\dot{q}_D)$
	$\tau = \tau_{ID}(\ddot{q}_D + \ddot{q}_{fb})$
	**Pros**
	PID is a constant
	**Cons**
	Computational expense of computing inverse dynamics
	Difficulty of calibrating accurate inertial parameters
# Links
[Section IV. DYNAMICS AND CONTROL](http://motion.cs.illinois.edu/RoboticSystems/RobotControl.html#Section-IV.-DYNAMICS-AND-CONTROL)

#robot_force_control #force_feedback