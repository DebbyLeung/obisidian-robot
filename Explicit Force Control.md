# Model of system
$m\ddot x =F_{gripper}+F_{env}$

$f_m=-F_{gripper}= d_s(\dot x−\dot{x_s}) +k_s(x−x_s)$
$f_e=-F_{env}=k_ex+d_e\dot x$

The aim is to control the force exerted to the environment $f_e$ in order to guarantee the stability of the grasp in micromanipulation, and also to not break components 
## Explicit
The explicit force control aims to control the force exerted on the environment $f_e$ in reference to a desired force $f_d$. Two types of explicit force control exist: force-based and inner position loop based.
	$f_e = f_d+Force\ controller*\epsilon +System*x_s -Force\ estimation*f_e$, where $\epsilon =f_d-f_e$
Fig.5 Explicit Force Control Loop
_______________________
$x_s=(-(f_d-f_e) -FC*\epsilon+FE*f_e)/SYS$
$x_s = -\frac{(1+FC)}{SYS}(f_d-f_e)+\frac{FE}{SYS}f_e$
$x_s = K_p(f_d-f_e)-K_d(\frac{d}{dt}){f_e}$
$x_s = K_p(f_d-f_e)-K_d(\dot{f_e})$

$K_p = -\frac{(1+FC)}{SYS},K_d(\frac{d}{dt}) = -\frac{FE}{SYS}$


## Impedance
$m\ddot x =F_{gripper}+F_{env}\ \&\  f_m=-F_{gripper}= d_s(\dot x−\dot{x_s}) +k_s(x−x_s)$ $ms^2X_s(s)+\frac{ms^2+d_ss+k_s}{d_ss+k_s}F_m(s)+F_e(s)=0$

## PD control
Hybrid force-position control
Usage: fixed position in one axis and *constant* force control in another axis
Example: Polishing
Impendance control aims to control dynamics of contact


# Links
https://hal.archives-ouvertes.fr/hal-00868627/document)
#robot_force_control #Impedance 
