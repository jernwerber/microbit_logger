# microbit_logger
We can build a data logger... we have the technology! Using Micropython, we can record and store data from the micro:bit's accelerometer as a file on the micro:bit itself, making use of the small amount of onboard non-volatile storage (nominally 512KB, but some of that gets used up by the program).

*Note: this functionality is now natively supported through the MakeCode micro:bit, so this repo is mostly for posterity's sake since there's probably an easier way to accomplish what this program does.*

This code has configuration parameters for:

- Changing the range of the values reported by the accelerometer to 2, 4 or 8G (default: 4G) by communicating with the micro:bit's IMU over `i2c`
- Setting a `sample_rate` (default: 10, which works out to 50 samples per second)
- Defining the duration (`dur`) that the micro:bit will log for (default: 5000 ms)
