# Port Status Check Script

## Overview
This script helps you check if a specific port is open, blocked, or in use. It verifies:
- Whether the port is actively listening.
- If the port is reachable.
- Which process is using the port.
- Whether firewall rules are blocking the port.
- Saves results in a log file for future reference.

## Features
- Uses `netstat`, `ss`, `nc (netcat)`, `lsof`, and `ufw` (if installed) to check port status.
- Outputs results to the terminal and logs them in `port_status_log.txt`.
- Works on Linux and MacOS.
- Requires `sudo` for firewall checks.

## Installation
1. Download the script:
   ```bash
   wget -O check_port_status.sh "https://raw.githubusercontent.com/your-repo/path/to/check_port_status.sh"
   ```
   or
   ```bash
   curl -o check_port_status.sh "https://raw.githubusercontent.com/your-repo/path/to/check_port_status.sh"
   ```

2. Give it execution permission:
   ```bash
   chmod +x check_port_status.sh
   ```

## Usage
Run the script with a port number:
```bash
./check_port_status.sh 5555
```

## Output Example
If port **5555** is open, you'll see something like this:
```
🔹 Checking Listening Ports (netstat)...
tcp        0      0 0.0.0.0:5555            0.0.0.0:*               LISTEN      1234/python3

🔹 Checking if Port is Reachable (nc)...
Connection to 127.0.0.1 5555 port [tcp/*] succeeded!

🔹 Checking Running Services (lsof)...
nc       1234 user  5u  IPv4 12345678  0t0  TCP *:5555 (LISTEN)

🔹 Checking Firewall Rules...
5555/tcp ALLOW Anywhere

✅ Check completed! Results saved in port_status_log.txt
```

## Troubleshooting
- If no output appears, the port may not be open.
- If you see `Connection refused`, the application may not be running or is blocked by the firewall.
- Use `sudo ufw allow 5555` to allow the port (if using UFW).

## License
This script is open-source and can be modified or distributed under the MIT License.

## Author
Developed by Amu Hlongwane, PHD Quantitative Analytics.
