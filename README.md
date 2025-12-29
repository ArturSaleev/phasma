# Phasma

**Phasma** is a lightweight CLI tool for automatic SSH port forwarding.
It helps you access remote databases and internal services locally as if they were running on your machine.

No Docker. No complex setup. Just SSH.

---

## When Phasma is useful

- Databases or services are accessible only via SSH or VPN
- You need multiple SSH port forwards running at the same time
- You want a simple way to share access configuration with your team
- You are tired of manually creating SSH tunnels

---

## How it works

1. Download a binary for your operating system
2. Download the example `config.json` from this repository
3. Edit `config.json` according to your infrastructure
4. Run the Phasma binary
5. Phasma connects to the server and forwards ports automatically


Phasma expects `config.json` to be located in the same directory as the binary.
---

## Which binary should I download?

Choose the binary according to your operating system and CPU architecture:

| Operating System | Architecture | File name |
|------------------|-------------|-----------|
| macOS (Intel)    | amd64       | `phasma_darwin_amd64` |
| macOS (Apple Silicon M1/M2/M3) | arm64 | `phasma_darwin_arm64` |
| Linux (x86_64)   | amd64       | `phasma_linux_amd64` |
| Linux (ARM64)    | arm64       | `phasma_linux_arm64` |
| Windows (x86_64) | amd64       | `phasma_windows_amd64.exe` |
| Windows (ARM64)  | arm64       | `phasma_windows_arm64.exe` |

After downloading, make the file executable (macOS/Linux):

---

## Usage

**Phasma** will:

- establish SSH connections
- forward all configured ports
- automatically reconnect if the connection is lost

## Configuration

**Phasma** uses a single config.json file.

SSH authentication with private key
```json
{
  "servers": [
    {
      "name": "main-server",
      "ssh": {
        "user": "TestServer",
        "host": "10.10.10.10:22",
        "private_key": "/Users/name/.ssh/ssh_key.key"
      },
      "forwards": [
        {
          "local": "127.0.0.1:13306",
          "remote": "10.81.81.2:3306",
          "description": "MySQL test"
        },
        {
          "local": "127.0.0.1:6379",
          "remote": "10.81.81.6:6379",
          "description": "Redis test"
        }
      ]
    }
  ]
}
```

SSH authentication with login and password
```json
{
  "servers": [
    {
      "name": "main-server",
      "ssh": {
        "user": "root",
        "host": "192.168.1.5:22",
        "password": "superpass"
      },
      "forwards": [
        {
          "local": "127.0.0.1:13306",
          "remote": "10.10.10.10:3306",
          "description": "MySQL test"
        },
        {
          "local": "127.0.0.1:6379",
          "remote": "10.10.10.10:6379",
          "description": "Redis test"
        }
      ]
    }
  ]
}
```

## Notes

- Phasma does not manage VPN connections
- VPN (if required) must be connected manually
- SSH credentials are read from the configuration file
- No external dependencies required

## Source Code

The source code is currently maintained in a private repository.

This public repository is used to distribute precompiled binaries
and collect user feedback.

## License

MIT License
