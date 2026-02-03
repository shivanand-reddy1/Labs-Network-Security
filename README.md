# Lab3a: Socket Programming - Client-Server Communication

## Overview

This lab demonstrates basic socket programming with a client-server architecture where a server runs on WSL (Windows Subsystem for Linux) and a client runs on Windows. The programs establish a TCP connection and exchange messages, implementing a simple echo server.

## Project Structure

```
lab3/
├── src/                              # Source code directory
│   ├── Lab3a_server_Win.py          # Server program (runs on WSL/Ubuntu)
│   └── Lab3a_client_WSL.py          # Client program (runs on Windows)
├── output/                           # Lab output and documentation
│   └── Lab3_1RVU23CSE431.pdf        # Lab report/submission
├── reference/                        # Reference materials
│   └── NetSec_Lab3_RVU.pptx         # Lab presentation/instructions
└── README.md                         # This file
```

## Files Description

### src/Lab3a_server_Win.py

**Purpose:** TCP server that listens for incoming connections and echoes back received data.

**Key Features:**

- Binds to all network interfaces (`0.0.0.0`)
- Listens on port 65432
- Displays network details (hostname, IP address, FQDN)
- Accepts client connections
- Receives data and echoes it back to the client
- Implements echo server functionality
- Runs in a loop to handle incoming data

**Network Configuration:**

- Host: `0.0.0.0` (all interfaces)
- Port: `65432`

### src/Lab3a_client_WSL.py

**Purpose:** TCP client that connects to the server and sends/receives messages.

**Key Features:**

- Connects to WSL server using specific IP address
- Displays network details (hostname, IP address, FQDN)
- Sends "Hello, server!" message to the server
- Receives and displays the echoed response
- Automatically closes connection after communication

**Network Configuration:**

- Server Host: `172.26.112.1` (WSL IP - must be configured based on your WSL setup)
- Server Port: `65432`

### output/Lab3_1RVU23CSE431.pdf

Lab report documenting the experiment results, observations, and analysis for RVU23CSE431.

### reference/NetSec_Lab3_RVU.pptx

Reference presentation containing lab instructions, objectives, and theoretical background for the network security lab

## Setup Instructions

### Prerequisites

- Python 3.x installed on both Windows and WSL
- WSL (Ubuntu or similar distribution) installed on Windows
- Network connectivity between Windows and WSL

### Configuration Steps

1. **Find WSL IP Address:**
   - In WSL terminal, run:
     ```bash
     ip addr
     ```
   - Look for the `eth0` interface IP address (e.g., `172.26.112.9`)

2. **Update Client Configuration:**
   - Open `src/Lab3a_client_WSL.py`
   - Update the `HOST` variable with the WSL IP address from step 1:
     ```python
     HOST = '172.26.112.1'  # Replace with your WSL IP
     ```

## Running the Programs

### Step 1: Start the Server (on WSL)

```bash
# Navigate to the lab3 src directory
cd /mnt/c/Users/shiva/college\ Work/lab3/src

# Run the server
python3 Lab3a_server_Win.py
```

**Expected Output:**

```
Lab1: Exp0:Server running on WSL: Welcome !!!
Host name:  <hostname>
IP address:  <ip-address>
FQDN:  <fqdn>
Server listening on 0.0.0.0:65432
```

### Step 2: Run the Client (on Windows)

```cmd
# Navigate to the lab3 src directory
cd C:\Users\shiva\College Work\lab3\src

# Run the client
py Lab3a_client_WSL.py
```

**Expected Output:**

```
Lab1: Exp0:Client running on Windows: Welcome !!!
Host name:  Shiva
IP address:  10.17.19.230
FQDN:  Shiva.RVU.local
Received Hello, server! from server
```

## How It Works

1. **Server Startup:**
   - Server binds to port 65432 on all network interfaces
   - Enters listening mode, waiting for client connections

2. **Client Connection:**
   - Client creates a TCP socket
   - Connects to server using WSL IP address and port 65432
   - Sends "Hello, server!" message as bytes

3. **Data Exchange:**
   - Server accepts the connection
   - Server receives the message from client
   - Server echoes the message back to the client
   - Client receives and displays the echoed message

4. **Connection Termination:**
   - Client closes the socket after receiving response
   - Server continues running, waiting for new connections

## Network Details Functions

Both programs include a `getNetworkDetails()` function that displays:

- **Hostname:** Computer's network name
- **IP Address:** Local IP address
- **FQDN:** Fully Qualified Domain Name

## Technical Specifications

### Protocol

- **Transport Protocol:** TCP (Transmission Control Protocol)
- **Socket Family:** AF_INET (IPv4)
- **Socket Type:** SOCK_STREAM (connection-oriented)

### Communication Flow

```
Client                          Server
  |                               |
  |-------- Connect ------------->|
  |                               |
  |---- "Hello, server!" -------->|
  |                               |
  |<--- "Hello, server!" ---------|
  |                               |
  |-------- Disconnect ---------->|
```

## Troubleshooting

### Common Issues

1. **Connection Refused:**
   - Ensure the server is running before starting the client
   - Check that the WSL IP address in the client matches the server's IP

2. **Port Already in Use:**
   - Change the `PORT` variable to a different value (e.g., 65433)
   - Ensure both client and server use the same port number

3. **Firewall Issues:**
   - Ensure Windows Firewall allows Python connections
   - WSL and Windows should have network connectivity

4. **Wrong IP Address:**
   - Run `ip addr` in WSL to verify the correct IP address
   - Update the `HOST` variable in the client code accordingly

## Project Documentation

- **Lab Report:** See [output/Lab3_1RVU23CSE431.pdf](output/Lab3_1RVU23CSE431.pdf) for detailed experimental results and analysis
- **Reference Material:** See [reference/NetSec_Lab3_RVU.pptx](reference/NetSec_Lab3_RVU.pptx) for lab objectives and instructions

## Learning Objectives

This lab demonstrates:

- Basic TCP socket programming in Python
- Client-server architecture
- Network communication between Windows and WSL
- Socket methods: `socket()`, `bind()`, `listen()`, `accept()`, `connect()`, `send()`, `recv()`
- Network information retrieval using socket module (hostname, IP, FQDN)
- Cross-platform networking
- Echo server implementation

## Key Concepts Covered

- **TCP/IP Protocol:** Connection-oriented, reliable data transmission
- **Client-Server Model:** Asymmetric communication pattern
- **Socket Programming:** Low-level network communication
- **WSL Networking:** Bridged network connectivity between Windows and Linux subsystem
- **Port Binding:** Listening on specific network ports
- **Data Serialization:** Converting strings to bytes for network transmission

## Future Enhancements

Potential improvements:

- Implement bi-directional communication (chat application)
- Add error handling and exception management
- Support multiple concurrent clients using threading or asyncio
- Implement custom protocols beyond echo
- Add logging functionality for debugging and monitoring
- Create configuration files for network settings
- Implement authentication and encryption (SSL/TLS)
- Add command-line argument parsing for flexible configuration

## Course Information

- **Course:** Network Security Laboratory
- **Lab Number:** Lab 3a
- **Student ID:** RVU23CSE431
- **Institution:** RVU (Reva University)
- **Date:** January 2026

## References

- Python Socket Programming Documentation: https://docs.python.org/3/library/socket.html
- TCP/IP Networking Basics
- WSL Networking Configuration Guide
- Network Security Fundamentals

---

**Lab:** Lab3a - Socket Programming  
**Platform:** Windows + WSL (Ubuntu)  
**Language:** Python 3.x  
**Author:** Shiva  
**Last Updated:** January 29, 2026
