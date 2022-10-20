# Introduction
 **Impedance control**
	 The "zero gravity mode" where the end effector behaves like a free-floating rigid body.

_____________________________
# Implicit control

Force- torque control with input of external force and retain position through calculation of Hooke's Law.
$F_{sensed} = F_{ext} + F_{gravity} + F_{inertial}=F_{ext}+mgsin({\theta})+[k(θ-θ_0 )+c ({\theta}'(t))│_{θ=θ_0}]$
+ $k$ = spring coefficient (stiffness)
+ $c$= damping coefficient
+ $F_{ext}$=  force applied


No load: $F_{sensed}=0+F_{gc}+0$
No motion with external force: $F_{sensed}=F_{ext}+F_{gravity}+0$
Moving: $F_{sensed} = 0 + F_{gravity} + F_{inertial}$


![Robotics 2 - Impedance Control](https://youtu.be/IolG5V_skv8?t=1193)

# Feedback approach
### Joint Current sensor

Current estimation of joints
Limitation: hard to linearize friction model 

### Joint Torque sensor

Receive signal directly from sensor, it avoids complicated calculation, i.e., friction model 
Limitation: Costly, bulky
Usage: UR series

### End-effector torque sensor/Base torque sensor

Solve force-torque vectors of each joints by inverse kinematic calculation by a sensor either at the end or base
Limitation: Accuracy is limited by inverse kinematic algorithm
Usage: 

### Harmonic Drive Estimation
Calculate harmonic gear deformation
Limitation: Complicated harmonic damping wave
Usage: Kinova

### Serial Elastic Actuator (SEA)
Integration of both displacement and torque information  to get the most accurate force-torque feedback
Limitation: costly, bulky
Usage: KUKA

### EMG

Receive biometric signal from human as interactive force 
Limitation: lower accuracy
Usage: Prothetic arm robot

#Impedance #robot_force_control
