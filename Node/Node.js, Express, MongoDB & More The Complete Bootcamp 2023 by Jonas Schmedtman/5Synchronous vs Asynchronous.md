# Synchronous vs Asynchronous code (Blocking vs Non-Blocking)

## Synchronous - execute the code one after another line.
* Each line of code basically waits for the result of previous line. This can be a problem in slow operations. One single line can slow whole code. Solution for this issue is ==Asynchronous/Non-blocking code==

## Asynchronous - 
* We upload heavy work to the background and once work is done call back function that we registered before will handle the result. During whole that time rest of the code is executing.

# Why Nodejs needs Asynchronous?

* Nodejs process is a single treaded.
* All the user accessing the system in same tread.


