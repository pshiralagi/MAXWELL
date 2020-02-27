---
authors: Lea Chandler;Chadd Miller;Pavan Shiralagi
date: 27th February 2020
---



# C&DH Code Breakdown:artificial_satellite:

### The Command and Data Handling Module is the brain of a satellite.   It is responsible for relaying data between various subsystems and decision making.

------------------------------------------------------------------------



### **`config_globals.h`**

***This header file contains various defines to access or restrict existing functionality in the C&DH code.***



### **`main.c`**

There are two primary modes - 

`FLIGHT_MODE` - Is the actual code that will be run.  It initializes tasks and sticks to the task-slot times.

`TEST_MODE` - Used for various tests.  It initializes flight application but does not start any tasks.  Used to ensure functionality of C&DH board.   After `flightApplicationStart()`, it just sits in a while loop blinking an LED.

 

```c
flightApplicationInit();
```

This function is called in both of the primary modes.  It initializes -

* IO Ports
* Timers
* UARTs 1 to 4
* I2C 1 and 2
* SPI 1
* Sensor drivers 
* ADCS
* Initializes spacecraft mode, boots to sleep state (looks like some sort of state machine)
* Ground contact watchdog, initializes communication

Various initializes occur, seems like a lot of different functions some with very similar explanations.



```c
flightApplicationStart();
```

This function is called in `FLIGHT_MODE` which begins by calling `flightApplicationInit()` and then contains the forever loop with the task-slot algorithm.



### **`taskslots.c`**















