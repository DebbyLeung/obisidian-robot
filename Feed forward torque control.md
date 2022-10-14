# Cons of PID controller in tq ctrl
1.  Gravity biases the torques needed to keep the robot upright. A PID controller compensates for gravity via the integral term, if a joint axis flips orientation, the torque needed is reverse.
2.  The effective inertia of the subchain at each joint is highly dependent on its configuration. For example, if an arm is outstretched, the shoulder joint will need to apply stiffer torques to track a trajectory than if it is tucked.
3.  At high speed, the Coriolis term becomes significant, causing biasing torques that must be compensated.
# Links
[Section IV. DYNAMICS AND CONTROL](http://motion.cs.illinois.edu/RoboticSystems/RobotControl.html#Section-IV.-DYNAMICS-AND-CONTROL)