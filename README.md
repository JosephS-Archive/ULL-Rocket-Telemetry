# ULL-Rocket-Telemetry
Firmware developed for the University of Louisiana at Lafayette (ULL) ULift Rocketry Team’s 2025 IREC sounding rocket. The system used an MPU6050 IMU and quaternion-based Madgwick sensor fusion to estimate rocket attitude, then transmitted pitch, roll, yaw, and barometric altitude over an SX1278 LoRa link to a ground station built by ULL’s CAPE team. It also logged attitude, altitude, temperature, pressure, and elapsed time to an SD card.

## Hardware

- LilyGO T-SIM7600 development board with ESP32 microcontroller
- MPU6050/MPU6500-family IMU for acceleration and angular-rate measurements
- BMP388 barometric pressure and temperature sensor
- SX1278 LoRa radio module for telemetry transmission
- MicroSD card and SD interface for onboard data logging (logging was not verified)
- ULL CAPE team ground station for receiving telemetry

## Dependencies

- Arduino IDE with the ESP32 board support package
- RadioLib 7.1.2
- MPU9250_WE 1.2.15 (`MPU6050_WE.h`)
- Adafruit BMP3XX Library 2.1.6
  - Adafruit Unified Sensor
  - Adafruit BusIO
- Time 1.6.1 (`TimeLib.h`)
- ESP32 core libraries: Wire, SPI, and SD

## Ground Testing

Ground tests evaluated attitude-estimation accuracy and the data-logging path. The team also tested altitude response in a parking garage and assessed radio communication range by carrying the payload around campus and driving around the city.

## Flight results

Confirmed communication on ground but lost communication at pad before launch

## Future work

- Complete and verify onboard SD-card logging, including data integrity checks and recovery of recorded files.
- Validate BMP388 altitude calculations against known elevations and improve baseline-pressure calibration.
- Configure LoRa parameters explicitly and measure communication range, packet loss, and reliability.
- Validate the MPU’s calibration against a precision tilt or rotation reference, and evaluate a lower-bias or 9-axis IMU with a magnetometer to improve attitude estimates and heading correction.
