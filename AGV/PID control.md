## Position loop control
![](https://ars.els-cdn.com/content/image/3-s2.0-B9780123859204000035-f03-22-9780123859204.jpg)
### PID controller
independent control of position, velocty, and current.
$u=K_p\epsilon+K_i\int\epsilon dt+K_d\dot{\epsilon}$
where $\epsilon(t)=y(t)-r(t)$, y(t) is output and r(t) as command.

P-proportional gain
I- improve transient reponse and reduce steady state error
D-improve damping, increase resistance to external disturbance

### In digital form
differtial term of $K_d = K_d\frac{e(t)-e(t-1)}{\Delta t}$
integral term of $K_i = K_i\sum_{t=0}^n{e(n-t)}{\Delta t}$


[PID controller](http://www.ee.ic.ac.uk/pcheung/teaching/de2_ee/Lecture%2018%20-%20PID%20controller%20%28x2%29.pdf)