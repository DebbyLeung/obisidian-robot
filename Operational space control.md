# Operational space control
 Controling the end effector of an articulated robot more accurately in Cartesian space than in joint space.
 
_Operational space control_ is a method for doing so without the use of inverse kinematics. It can also apply or respond to forces in Cartesian space which is a key step in #robot_force_control and #Impedance  control.

Task space: $x = \phi(q)$, Jacobian: $J(q) = \frac{\partial \phi}{\partial q}(q)$, where $q =\theta$
# Mathematical derivation
Let $u$ st. $q˙=u$, 
Let $x_D(t)$ be the ideal task space trajectory, $x=ϕ(q)$ be the current task space coordinate.

define a commanded task velocity 
$\dot{x}_{cmd} = -K_P (x - x_D(t)) + \dot{x}_D(t)$
$\dot{x} = J(q)\dot{q}$ 

Jacobian transpose rule: $u = \dot{q} = J(q)^T\dot{x}_{cmd}$
Task space error: $e = x - x_D \to \dot{e} = J \dot{q} = - J J^T K_P e.$


# Links
[Chapter 16. Control of Articulated Robots,Section IV. DYNAMICS AND CONTROL](http://motion.cs.illinois.edu/RoboticSystems/RobotControl.html#Section-IV.-DYNAMICS-AND-CONTROL)
https://motion.cs.illinois.edu/RoboticSystems/