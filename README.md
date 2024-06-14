SUNA V2 Autonomous Data Recording Scripts
These scripts are designed to autonomously record data from the SeaBird SUNA V2 using a Raspberry Pi.

Overview
The SeaBird SUNA V2 can operate in two modes: polled or continuous. Continuous operation significantly reduces the lifespan of the light source, making polled operation the preferred method due to the high cost of replacing bulbs.

Configuration
The script imports settings from an external configuration file (COM). This file includes the SUNA baud rate, serial number, and COM port. Using this configuration file allows you to easily adjust the COM ports when multiple instruments are connected to the same Raspberry Pi without modifying the main script.

Configuration Parameters:
Serial Number: Used to identify specific lines of data.
Baud Rate: Default is 57600.
COM Port: Typically assigned as /dev/ttyUSB*, where * corresponds to the order the device was connected, starting with 0.
Main Script Workflow
Set Data File Location: Define the data file location and assign it to the file variable.
Set Alarm: Configure an alarm to terminate the script if the sensor is unresponsive. This prevents multiple script instances from running simultaneously. Adjust the alarm duration to match your sampling frequency.
Open and Verify Port: Open the specified COM port and verify the connection.
Awaken SUNA:
If the SUNA is not in CMD mode, execute the exit command and attempt to re-enter CMD mode.
Send Measure Command: Use the command measure n where n is the number of samples to collect.
Read Output: Read output lines until the serial number is detected, then parse the line to extract the desired nitrate data.
Write Data: Write the parsed data to the specified file.
