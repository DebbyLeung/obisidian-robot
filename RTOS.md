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

use freeRTOS lib