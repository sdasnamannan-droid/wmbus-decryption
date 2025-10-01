
# WMBus Telegram Decryption (OMS Mode 5)

## Overview
This project implements AES-128-CBC decryption of a Wireless M-Bus (WMBus) telegram, following the OMS (Open Metering System) Volume 2 standard for Security Mode 5.

## Inputs
- **Telegram (encrypted):** Provided in `telegram.hex`
- **AES-128 Key:** Provided in `key.txt` (hex format, 32 characters)

## Process
1. Load the AES-128 key and telegram from input files.
2. Extract the 8-byte address and 1-byte access number from the telegram.
3. Construct the Initialization Vector (IV) as `[address (8 bytes)] + [access number repeated 8 times]`.
4. Decrypt the ciphertext starting from byte 18 using AES-128-CBC with the given key and IV.
5. Verify decryption by checking that the plaintext begins with `2F 2F`.

## Example Run
Command to build and run:
```bash
g++ -std=c++17 wmbus_decrypt.cpp -o wmbus_decrypt -lcrypto
./wmbus_decrypt
