# Xray CLI

Simple command-line tool to manage Xray proxy on Linux.

## Features
- ✅ Parse vless:// URLs automatically
- ✅ Start/stop Xray proxy easily
- ✅ TUN mode for system-wide routing
- ✅ Status checking
- ✅ Run apps with proxy

## Requirements
- Xray core
- redsocks (for TUN mode)
- Python 3.6+

## Installation

### 1. Install dependencies

**Xray:**
```bash
sudo bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```

**Redsocks:**
```bash
# Arch/Manjaro
yay -S redsocks

# Ubuntu/Debian
sudo apt install redsocks
```

### 2. Install xray-cli
```bash
sudo curl -L https://raw.githubusercontent.com/clkwee/xray-cli/main/xray-cli -o /usr/local/bin/xray-cli
sudo chmod +x /usr/local/bin/xray-cli
```

### 3. Create redsocks config
```bash
sudo nano /etc/redsocks.conf
```

Paste this:
```
base {
  log_debug = on;
  log_info = on;
  log = "file:/var/log/redsocks.log";
  daemon = on;
  redirector = iptables;
}
redsocks {
  local_ip = 127.0.0.1;
  local_port = 2525;
  ip = 127.0.0.1;
  port = 1080;
  type = socks5;
}
```

## Usage

### First time setup
```bash
# Get your vless:// config
xray-cli get-config "vless://your-config-here"

# Check status
xray-cli status
```

### Start proxy
```bash
sudo xray-cli proxy start
```

### Enable system-wide routing (TUN mode)
```bash
sudo xray-cli tun start
```

### Run specific app with proxy
```bash
xray-cli run firefox
xray-cli run chromium
```

### Stop everything
```bash
sudo xray-cli tun stop
sudo xray-cli proxy stop
```

## Commands

- `get-config <url>` - Download and save vless:// config
- `status` - Show current status
- `proxy start` - Start Xray proxy
- `proxy stop` - Stop Xray proxy
- `tun start` - Enable TUN mode (routes all traffic)
- `tun stop` - Disable TUN mode
- `run <app>` - Run app with proxy

## Notes
This tool was created with AI assistance (Claude) based on my existing bash scripts and requirements.

## License
MIT
