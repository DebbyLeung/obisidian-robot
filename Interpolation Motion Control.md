# Trajectory following

*We want a desired joint space trajectory $qD(t)$ approch to the robot's actual trajectory $q(t)$*
### Rules
1. discontinuities in $qD(t)$ = will accelerate quickly, and possibly **overshoot** the target. 
2. discontinuities in $qD'(t)$ = require instantaneous acceleration. Sudden changes of velocity runs the risk of **overheating** motors and **overshooting setpoints**.
3. joint stops and self-collision should be avoided with some **margin of error**, since the controller will not execute the trajectory exactly, especially at high speed. The magnitude of the margins should be chosen proportionally to the magnitude of control errors, which depend on the stiffness of the underlying controller.

## Motion queue
![](http://motion.cs.illinois.edu/RoboticSystems/figures/control/motion_queue.svg)
Figure 2. Illustrating a 3-axis motion queue.
___________
Setpoint of desired joint values ${\theta}_D$ and ${\theta}'_D$ is sent to PID controller. Controller maintains future setpoints in its memory. Future trajectory can be modified externally.



!!!!!!!!!!!!! For example, adding a Go-To request will append an interpolating curve from the end of the queued trajectory to the requested target position (a _waypoint_). If the current queue is empty, then the curve will originate from the current robot position.!!!!!!!!!!

## Interpolation profiles
Given the robot at rest and a target configuration, an _interpolation profile_ is a continuous trajectory that satisfies certain operational constraints on the robot's joint dynamics. A sequence of Go-To commands can be implemented by concatenating several interpolation profiles, in which the robot stops/starts at subsequent waypoint configurations.
### Piecewise linear
Basic linear curve by constraining $v_{max}$. It allows instantaneous changes of velocity.
![](http://motion.cs.illinois.edu/RoboticSystems/figures/control/linear_interpolation.svg)
Figure 3. Illustrating the use of piecewise linear interpolation profiles. 
	At time $t_0$, a commanded waypoint $θ_g$ is sent, and an interpolating curve is constructed (left). 
	At time $t_1$, a new waypoint command $θ_{g2}$ is sent that interrupts execution of the existing curve cause recalculation of interpolating curve (right). 
___

### Trapezoidal velocity profile
Duration of curve $t_f$ is calculated with displacement between start and goal, bounded by $v_{max}$ and $a_{max}$.
For 2 segments scenario, 
	$(\frac{{\theta}_g -{\theta}_s)}{2}=\frac{1}{2} a_{max}(t_f/2)^2 \to t_f=2\sqrt{(θg−θs)/a_{max}}$ (eq. 1)
When midpoint velocity $a_{max}t_f/2 >v_{max}$, we need to divide into 3 segments ,	
	In $[t_0, t_3]$, since acceleration time is equal to deceleration time, $t_1 = t_3$ and $t_1=v_{max}/a_{max}$, then ${\theta}_1-{\theta}_s =v_{max}^2/(2a_{max})$, so $t_2=(θg−θs)/v_{max}-v_{max}/a_{max}$
	$t_f=2t_1+t_2=(θg−θs)/v_{max}+v_{max}/a_{max}$       (eq. 2)

![](http://motion.cs.illinois.edu/RoboticSystems/figures/control/trapezoidal_velocity_profile.svg)
Figure 4. Trapezoidal velocity profile interpolation of 3 segments.
	The joint trajectory switches between parabolic, linear, and parabolic segments(Left).
	Velocity-time graph is a trapezoidal velocity pulse with velocity restrcited  
___

#### Bounded-jerk interpolation
Determination of the number of segments, segment timing, and overall duration is similar to the above construction, although higher-order polynomials need to be solved.
#### General methods and cubic curves
##### Cubic curve
For example, a cubic curve $θ(u)$ interpolating between $θ_s$ and $θ_g$ over the range $u∈[0,1]$ has the form,
$$
θ(u)=θs+(θg−θs)(a+bu+cu^2+du^3)
$$

Using the boundary conditions 
``
$$
\begin{cases}
θ(0)=θs\\ 
θ(1)=θg\\
θ′(0)=0\\
θ′(1)=0
\end{cases}
\to
\begin{cases}
a=0\\
a+b+c+d=1\\
b=0\\
b+2c+3d=0.\\
\end{cases}
$$

Then, $a=0, b=0, c=3, d=−2$
$$
θ(u)=θs+(θg−θs)(3u^2-2u^3)
$$

$v_{max} @ t=t_f/2$, $a_{max} @ t=t_f$, So 

$θ'(t)=θ'(u(t))u'(t)=(θ_g−θ_s)(6u−6u^2)/t_f=6(θ_g−θ_s)(t/t_f^2−t^2/t_f^3)$
$\to v_{max}=θ'(t_f/2)=\frac{3}{2}(θ_g−θ_s)/t_f$
$θ''(t)=6(θ_g−θ_s)(1/t_f^2−2t/t_f^3)$
$\to a_{max}=θ''(t_f)=6(θ_g−θ_s)/t_f^2$

## Speed and velocity control
control displacement by velocity, hard to modify instantaneously
## Cartesian commands
IK solution required, might hits joint limit or passes near sigularities
![](http://motion.cs.illinois.edu/RoboticSystems/figures/control/cartesian_queuing.svg)
Figure 5. A motor controller may mix Cartesian and joint-space motion queuing.
	Left: the end effector trace of a 2R manipulator with a mixture of joint space (solid) and Cartesian space (dotted) waypoint commands. 
	Right: the same trace, but in joint space.
## Interruption
help with motion queuing, rarely implemented for most industrial robots.
Options
1.  slows down each joint as quickly as possible.
	1. cons: drift from the desired trajectory because each joint is slowed at a different rate, which may cause collisions.
2. instantaneously start moving to a new waypoint, clearing the remainder of the queue
## State machines
used in system integration
![](http://motion.cs.illinois.edu/RoboticSystems/figures/control/state_machine.svg)
Figure 6. 
	Left: A state machine is a directed graph that describes the discrete modes that a controller can switch between. 
	Right: An example state machine for a controller that detects hardware faults and can switch between joint space commands, Cartesian commands, and braking commands.


# Links
[Section IV. DYNAMICS AND CONTROL](http://motion.cs.illinois.edu/RoboticSystems/RobotControl.html#Section-IV.-DYNAMICS-AND-CONTROL)
#position_control