#### difficulties of navigation
- hard to find out the precise location in poor network
- allocation order tasks efficiently
## Scene 
### Sync server and robots information
#### Map
For server: information of all robots
For robot: map info *at the particular* scene
##### Not sync
- map not exist
- map is different from the existing map
#### Robot group and label
Same group = same map, same type of agv
Same label = can be different mechanism
**Astar planning**
# MAPF
#### Restrictions
- path intersect w/o setting a nav point
- width of robot collide each other

Execution time : weighted point x distance length + curvature, rotation, jamming
#### Main feature
+ Confidence: the higher the more time spend, the more efficient
+ CustomizedAstar: 
	+ curvature: time needed to steer is more, increased weight of the selection
	+ queuing : if AMR stopped, it costs more time in total
+ Dispatching Length: higher the length, the shorter execution time, the more resources(locations in the map) are reserved. **TO FIND THE SWEET POINT BETWEEN DRIVING EIFFICIENCY AND SHORTEST PATH**
#### Other param
- collision checking.
- main path decision making
- auto queuing restricted path
- auto replan
#### Avoid blocking(gmap off)
Request for free navigation with in the avoiding region. and mutex that region.
#### Mutex
Only one point at a time can be reserved in the mutex region.

# AGV selection logic
```python
class Car:
	self.label =label
def serach_label(cars):
	rule1 = []
	for car in cars:
		if car.label == label or location or fromLoc or toLoc:
		  rule1.append(car)
	return rule1
def single_order(rule1):
	pointing_of_agv_effieciency(rules1)
def joint_order(rule1, order):
	rule2 = []
	for car in rule1:
		if car.toLoc-target <= JoinableDist:
		  rule2.append(car)
	agv_to_pick = np.array(rule2).min()
	agv_to_pick.pick_order(order) 
```
assign jobs(max=100) to n-cars according to, 

$Value_{total}=Value_{order}+Value_{car}$ in ascending order. 
where $Value_{order}=−P⋅R_p​−T⋅R_t​$ for expected value of priority and scheduled time & $Value_{car}=D⋅R_d​−V⋅R_v$ for expected value of distance and delivery time.

when there is one order,
$$

\begin{bmatrix}Val_1\\Val_2\\\vdots \\Val_n\end{bmatrix}=\begin{bmatrix} D_1\\D_2\\\vdots\\D_n\end{bmatrix}R_d-\begin{bmatrix} P_1\\P_2\\\vdots\\P_n\end{bmatrix}R_p-\begin{bmatrix} T_1\\T_2\\\vdots\\T_n\end{bmatrix}R_t-\begin{bmatrix} V_1\\V_2\\\vdots\\V_n\end{bmatrix}R_v
$$
choose the min value
when there are 100 orders,
$$\begin{bmatrix}Val_{11}&Val_{12} \dots \\
    \vdots & \ddots & \\\\Val_{1n}&&Val_{100n}\end{bmatrix}$$
choose the min value then eliminate the row and loop for 100 cycles until each amr gets one order.
```python
import numpy as np

def get_argmin(matrix):
    # Initialize lists to store the row and column indices
    result_indices = []
    seq_order = []
    r,c = matrix.shape

    # Iterate until you get 100 results
    while c > 1:
        for i in range(r):
            # Find the indices of the minimum value in the matrix
            min_indices = np.unravel_index(np.nanargmin(matrix[i]), matrix.shape)
            # Append the row and column indices to the result_indices list
            result_indices.append((i,min_indices[1]))
            matrix[ :, min_indices[1]] = np.nan
            c -=1
        seq_order.append(result_indices)
        result_indices = []
    return seq_order

car =10
order = 100
seq_orders = get_argmin(np.random.rand(car, order))

for seq_order in seq_orders:
    print(seq_order)

```

# Links
[AvoidObsRegion](https://seer-group.yuque.com/pf4yvd/gp9mgx/fb4liu?singleDoc#)
