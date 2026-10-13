# ULL Rocket Telemetry Payload

## Project Overview

This project developed a telemetry payload for the University of Louisiana at Lafayette (ULL) ULift Rocketry Team’s 2025 IREC sounding rocket. The payload used an ESP32-based LilyGO T-SIM7600 board, an MPU6050-family IMU, a BMP388 barometric sensor, and an SX1278 LoRa radio.

Firmware estimates the rocket’s pitch, roll, and yaw using quaternion-based sensor-fusion logic. It reads barometric altitude and sends the attitude and altitude values to a ground station built by ULL’s CAPE team.

Hardware/software was developed for use by ULL's rocketry team as well as CAPE for sounding rockets and weather balloon applications.

## How the System Works

At startup, the firmware initializes the sensors and radio, calibrates the IMU offsets, and establishes a barometric reference. Keep the payload stationary during startup calibration.

While running, the firmware:

- Reads acceleration and angular-rate data from the IMU.
- Estimates pitch, roll, and yaw.
- Reads pressure and temperature from the BMP388 and calculates relative altitude.
- Prints pitch, roll, yaw, and altitude to the serial connection.
- Transmits those four values over LoRa for reception by the ground station.
- Attempts to append telemetry and sensor readings to a microSD card. SD-card logging was not verified.

The transmitted readings are formatted as comma-separated values:

```text
pitch,roll,yaw,altitude
```

The radio helper appends a packet counter to the transmitted payload.

## Hardware

- LilyGO T-SIM7600 development board with ESP32 microcontroller
- MPU6050/MPU6500-family IMU
- BMP388 barometric pressure and temperature sensor
- SX1278 LoRa radio module
- MicroSD card and interface for attempted onboard data logging

## General Use

1. Assemble the payload with the IMU, barometer, LoRa radio, antenna, and power source. 
2. Upload the firmware to the ESP32
3. Power on the payload while it is stationary and allow startup calibration to finish.
4. Run the compatible ground station to receive and view the LoRa telemetry.
5. Monitor the serial output during ground testing to inspect the transmitted attitude and altitude values.

## Ground Testing and Flight Outcome

Ground testing included checks of attitude estimates and the data-logging path, altitude-response tests in a parking garage, and LoRa communication tests while walking around campus and driving around the surrounding area.

Communication was confirmed during ground testing, but the link was lost at the launch pad before liftoff. The project did not produce confirmed in-flight telemetry.

## Known Limitations and Future Work

- Onboard SD-card logging was not verified; recorded files and data integrity should be checked before relying on it.
- Attitude and altitude testing did not produce documented accuracy measurements.
- Yaw is estimated with a six-axis IMU and may drift over time; validate calibration against a reference and consider an IMU with a magnetometer.
- Measure LoRa range and packet reliability under controlled conditions.
- Validate barometric altitude against known elevations and improve the pressure-reference procedure.
