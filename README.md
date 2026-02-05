# Network Security Labs

A collection of network security lab experiments demonstrating socket programming and cryptographic implementations between Windows and WSL (Windows Subsystem for Linux).

## Project Structure

```
Labs-Network Security/
├── Lab3/
│   ├── materials/
│   ├── output/
│   └── src/
│       ├── Lab3a_client_WSL.py    # TCP client (runs on Windows)
│       └── Lab3a_server_Win.py    # TCP server (runs on WSL)
│
└── Lab4/
    ├── materials/
    ├── output/
    └── src/
        ├── Symmetric Key Ciphers/
        │   ├── client.py          # AES client (Windows)
        │   ├── server.c           # AES server (WSL)
        │   └── server             # Compiled server executable
        │
        └── Asymmetric Key Ciphers/
            ├── client.py          # RSA client (Windows)
            ├── server.c           # RSA server (WSL)
            └── asym_server        # Compiled server executable
```

## Lab 3: TCP Socket Programming

Basic client-server communication using TCP sockets across Windows and WSL.

### Features

- Network details retrieval (hostname, IP address, FQDN)
- TCP socket connection establishment
- Echo server implementation

### Running Lab 3

**On WSL (Server):**

```bash
python3 Lab3a_server_Win.py
```

**On Windows (Client):**

```bash
python Lab3a_client_WSL.py
```

> **Note:** Update the `HOST` variable in the client script with the WSL IP address (use `ifconfig` on WSL to find it).

---

## Lab 4: Cryptographic Implementations

### Experiment 1: Symmetric Key Cipher (AES-128-CBC)

Implements AES-128-CBC encryption/decryption for secure client-server communication.

#### Prerequisites

**On WSL:**

```bash
sudo apt-get update
sudo apt-get install libssl-dev
```

**On Windows:**

```bash
pip install cryptography
```

#### Configuration

- **Port:** 65431
- **Key:** `0123456789abcdef` (16 bytes)
- **IV:** `abcdef9876543210` (16 bytes)

#### Running

**Compile and run server on WSL:**

```bash
gcc server.c -lssl -lcrypto -o server
./server
```

**Run client on Windows:**

```bash
python client.py
```

---

### Experiment 2: Asymmetric Key Cipher (RSA)

Implements RSA public-key encryption for secure message exchange.

#### Prerequisites

**On WSL:**

```bash
sudo apt-get update
sudo apt-get install libssl-dev
```

**On Windows:**

```bash
pip install cryptography
```

#### Key Generation (on WSL)

Generate RSA key pair before running:

```bash
# Generate private key
openssl genpkey -algorithm RSA -out private.pem -pkeyopt rsa_keygen_bits:2048

# Extract public key
openssl rsa -pubout -in private.pem -out public.pem
```

> **Important:** Copy `public.pem` to the Windows directory where the client Python script is located.

#### Configuration

- **Port:** 65432
- **Key Size:** 2048-bit RSA
- **Padding:** PKCS1v15

#### Running

**Compile and run server on WSL:**

```bash
gcc server.c -lssl -lcrypto -o asym_server -Wno-deprecated-declarations
./asym_server
```

**Run client on Windows:**

```bash
python client.py
```

---

## Network Configuration

Both labs require proper network configuration between Windows and WSL:

1. Find WSL IP address:

   ```bash
   # On WSL
   ifconfig
   ```

2. Update the `HOST` variable in client scripts with the WSL IP address.

3. Ensure firewall rules allow traffic on the specified ports (65431, 65432).

## Technologies Used

| Component             | Technology       |
| --------------------- | ---------------- |
| Server Language       | C (with OpenSSL) |
| Client Language       | Python 3         |
| Symmetric Encryption  | AES-128-CBC      |
| Asymmetric Encryption | RSA-2048         |
| Network Protocol      | TCP/IP           |
| Python Crypto Library | cryptography     |

## Dependencies

### WSL

- GCC compiler
- OpenSSL development libraries (`libssl-dev`)
- Python 3

### Windows

- Python 3
- `cryptography` package

## License

This project is for educational purposes as part of Network Security coursework.
