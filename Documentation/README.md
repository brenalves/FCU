# Gravitum Flight Control Unit

That project actually is part of my conclusion project of Federal University of Fronteira Sul Computer Science Bachelor's degree.

The main purpose is create a circuit capable of run my code to support a navigation system for a fixed-wing airplane. The setted goal is takeoff from a field, navigate through a set of geographical waypoints with remote control and telemetry capabilities.

## Requisites
- Presence of sensors like a IMU (Inertial Measurement Unit) with gyroscope, accelerometer and magnetometer.
- Barometer for altitude measurement.
- GPS/GNSS (preference for GNSS) for waypoint interception.
- Logging via SD card for study and incidente analysis.
- Telemetry with a Ground Station (my notebook).
- Radio control with stable connection.
- Servo and engine(s) control.

## System
I did few searches in web and every previous FCU that I saw had 2 MCUs and are divided in Navigation Unit and Flight Control Unit, where the NU maybe are responsible for collect sensors (IMU, Baro, GNSS) data, perform some filtering or calculations needed and send to FCU.

FCU probably manages everything else like filtered data, flight plan, telemetry, PID calculations, servos and engine commands, etc.

I pretend to follow that approach because I don't overload the FCU doing filtering and data treatment, just focus the FCU in actually compute how to control the airplane. Furthermore that design allow use of a single serial protocol like UART or SPI (probably the faster one possible) to send all the sensor data already fine-tuned.

## Parts
- STM32F405RGT6 (FCU)
- STM32F303CCT6 (NU)
- ICM-20948 (IMU 9-axis)
- BMP390 (Barometer)
- u-blox NEO-M8N (GNSS)
- HappyModel EP1 (Radio Control)

## Anotations
1. I saw in HADESFCS that it uses a Voltage/Current shunt sensor (INA219AIDCNR) for battery measurements, I2C protocol. It's interesting.
2. HADESFCS uses the MIC26903 bulk regulator to convert the Vin to 5V.
3. It uses chain supply (12V -> 5V -> 3.3V), to reduce to 3.3V the 5V passes by LD39200PU33R (low drop regulator).
4. 12V passes to 5V using bulk regulator, 5V supplies the VCC PWM pins (Servos and ESC), the 5V is converted to 3.3V via linear regulator, 3.3V supplies the MCUs and the sensors.

## Questions to think about
- I don't know if I put the SD Card Receptacle already in board or just the connector.
- Probably I need an aileron, elevator, rudder, wheel, and two general purpose PWM channel with 5V supply.
- Radio will be a separate board so I need JST-SH 4 pins socket to connect it.
- The ESC's 5V PWM pins need some type of back-supply protection? Because it has a BEC to supply the circuit but its useless.
- WTF are those Test Points in HADESFCS?
- The Reset push button capacitor in HADESFCS are for prevent bouncing? Idk.
- Why more decoupling capacitors in each VDD pin in MCU? I saw that the recommended are 3 if possible but at least 1 is necessary.
- What is the utility of R_ext in HSE (oscillator) circuit in HADESFCS.
- What is the utility of the Solder Jumpers in USB Programming section in HADESFCS.
- What is the difference of USB Programming and USB Debug in HADESFCS.