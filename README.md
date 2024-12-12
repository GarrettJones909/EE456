# EE-456 Raspberry Pi LoRa GPS Communication Project 

# Group Members: Garrett Jones, Warren Howard, Andrew Sakdikul, and Jason Mao

## Overview
This project implements a distributed GPS tracking system using Raspberry Pi and LoRa communication, consisting of three key components:
1. GPS Transmitter Pi
2. LoRa Client Pi
3. Server Pi

## System Architecture
The system works in a three-stage communication process:
1. **GPS Transmitter Pi**: 
   - Reads GPS coordinates from a serial GNSS module
   - Parses NMEA sentences
   - Transmits GPS data via LoRa radio

2. **LoRa Client Pi**:
   - Receives GPS coordinates from the LoRa radio
   - Establishes a TCP socket connection to the server
   - Forwards received GPS data to the server

3. **Server Pi**:
   - Listens for incoming socket connections
   - Receives GPS coordinates from the LoRa client
   - Logs or processes the received GPS data

## Hardware Requirements
- 3 Raspberry Pi units
- SX1262 LoRa radio module
- GNSS/GPS module
- PiHal library for radio communication

## Dependencies
- RadioLib
- PiHal
- C++ standard library
- Socket programming libraries

## Components

### 1. GPS Transmitter (`lora_gps_tx.cpp`)
- Opens serial port for GNSS module
- Reads and parses NMEA sentences
- Initializes SX1262 LoRa radio module
- Transmits GPS coordinates via LoRa

### 2. LoRa Client (`gps_lora_client.cpp`)
- Receives GPS coordinates via LoRa radio
- Establishes TCP socket connection
- Sends received GPS data to server

### 3. Server (`server.cpp`)
- Creates socket on port 8080
- Listens for incoming connections
- Receives and processes GPS data
- Sends acknowledgment to client

## Setup Instructions

### Prerequisites
1. Install RadioLib library
2. Install PiHal library
3. Configure Raspberry Pi for:
   - SPI communication
   - Serial GNSS module
   - Network connectivity

### Compilation
Compile each component:
```bash
g++ -o gps_transmitter lora_gps_tx.cpp.cpp -lRadioLib -lPiHal
g++ -o gps_lora_client gps_lora_client.cpp
g++ -o server server.cpp
```

### Configuration
- Set LoRa frequency (currently 915.0 MHz)
- Adjust IP addresses for network communication
- Configure serial port settings
- Set correct SPI pins for your Raspberry Pi model

## Communication Flow
1. GPS Transmitter reads coordinates
2. Coordinates transmitted via LoRa
3. LoRa Client receives coordinates
4. Client sends coordinates to Server
5. Server receives and processes data

## Frequency and Radio Parameters
- Frequency: 915.0 MHz
- Bandwidth: 125.0 kHz
- Spreading Factor: 7
- Sync Word: Private

## Notes
- Requires root/sudo privileges for hardware access
- Tested on Raspberry Pi Zero
- Modify radio parameters based on local regulations

## Potential Improvements
- Add error handling and logging
- Implement persistent connections
- Create web/mobile GPS tracking interface
- Add authentication for data transmission

## Troubleshooting
- Verify serial port configuration
- Check LoRa radio module connections
- Ensure consistent frequency across devices
- Verify server port configuration
  
## Contributors
Ben Duval - https://github.com/BenDuval
