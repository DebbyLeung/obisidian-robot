### Sensor fusion
fuse sensor data to improve localization accuracy

#### Accelerometer - long term
At rest, (ideal, X noise, time-variant )
$[a_x, a_y, a_z] =[g*sin(\theta), -g*cos(\theta)sin(\phi),-g*cos(\theta)cos(\phi),]$
$[\phi_{acc},\theta_{acc}]=[tan^{-1}(\frac{a_y}{a_z}),sin^{-1}(\frac{a_x}{g})]$
Problem:
no estimation during short period of time
### Gyroscope/IMU -short term
At rest, (ideal, X noise, time-variant )$$\begin{bmatrix} \dot{\phi}\\\dot{\theta} \end{bmatrix}=\begin{bmatrix} 1&sin(\phi)tan(\theta)&cos(\phi)tan(\theta)\\0 &cos(\phi)&-sin(\phi)\end{bmatrix}\begin{bmatrix} p\\q\\r \end{bmatrix}$$$[\int{\dot{\phi}}dt,\int{\dot{\theta}}dt]$ # error generate due to noise
Problem:
Gyro drift - error accumulate at steady state

# Complementary filter
Acc term $\cdot\alpha$+Gyro term integral $\cdot(1-\alpha)$+ error = output
& feedback error to integral [[PID controller]]

Gyro has a better estimation on realtime data, so mainly use Gyro Acc as an assistant

## State observer
$X_{u+1} = IX_u+scalar.T\cdot IU+scalar.\alpha\cdot (X_u-X_est)$

# Extended Kalman filter
EKF is the optimal way to select $\alpha$
# Links
[Sensor Fusion](https://www.youtube.com/watch?v=BUW2OdAtzBw)