### Intro
Often use in microcontrollers
Purpose: to meet very strict schedule and manage 
- Tasks cheduling
- device manager
- resource management (io) 

### Pros:
- runs tasks concurrently

### How it normally works?
#### Super Loop: setup + loop(task xn) + interrupt
Features: no concurrency, single thread
#### Rtos: + loop x n(parallel) + interrupt
Features: multithreads

Queue is used for reading values without missing items while reading
# Links
[Introduction to RTOS](https://www.youtube.com/watch?v=pHJ3lxOoWeI&list=PLEBQazB0HUyQ4hAPU1cJED6t3DU0h34bz&index=5)
use freeRTOS lib