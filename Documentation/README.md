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

## Questions to think about
- I don't know if I put the SD Card Receptacle already in board or just the connector
- Probably I need an aileron, elevator, rudder, wheel, and two general purpose PWM channel with 5V supply
- Radio will be a separate board so I need JST-SH 4 pins socket to connect it