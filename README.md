# Xray CLI

Simple command-line tool to manage Xray proxy on Linux with an easy interactive menu.

## Features

- ✅ **Interactive Menu** - Just run `xray-cli` for a beginner-friendly menu
- ✅ **Command-Line Mode** - Full command support for scripts and automation
- ✅ **Auto Setup** - One command to install Xray, Redsocks, and configure Redsocks
- ✅ **Autostart** - Enable Xray (and optionally TUN mode) to start on boot
- ✅ **Persistent TUN Mode** - Autostart remembers if you want TUN mode enabled
- ✅ Parse vless:// URLs automatically
- ✅ Start/stop Xray proxy easily
- ✅ TUN mode for system-wide routing
- ✅ Status checking with emojis
- ✅ Run apps with proxy (working strange for now)
- ✅ Restart proxy with one command

## Requirements

- Xray core
- redsocks (for TUN mode)
- Python 3.6+

## Installation

### 1. Auto Setup (Recommended)

This will install Xray, redsocks, and create the redsocks config file for you.

```bash
sudo xray-cli install-everything
```

### 2. Manual Installation (if not using Auto Setup)

#### Install dependencies

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

#### Install xray-cli

```bash
sudo curl -L https://raw.githubusercontent.com/hhaxar/xray-cli/main/xray-cli -o /usr/local/bin/xray-cli
sudo chmod +x /usr/local/bin/xray-cli
```

#### Create redsocks config (if not using auto setup)

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

### Interactive Menu (Easiest)

Just run without any commands:

```bash
# For read-only actions (status, get-config)
xray-cli

# For actions that need root (start/stop proxy, TUN mode, install, autostart)
sudo xray-cli
```

You'll see a menu like this:

```
==================================================
🔍 Xray CLI - Interactive Menu
==================================================

ℹ 💡 Config: 1.2.3.4:443
✓ ✨ Proxy: Running 🚀
ℹ 💡 TUN: Disabled 🔓
✓ ✨ Autostart: On 🔄

==================================================
📋 Menu Options:
==================================================

  1. 📊 Show Detailed Status
  2. 🚀 Start Proxy
  3. 🛑 Stop Proxy
  4. 🛡️  Enable TUN Mode
  5. 🔓 Disable TUN Mode
  6. 📥 Get/Update Config
  7. 🏃 Run App with Proxy
  8. 🔄 Restart Proxy
  9. 🔁 Enable Autostart
 10. 🚫 Disable Autostart
 11. 📦 Install Everything (Auto Setup)
 12. ❌ Exit

==================================================

💡 Choose option (1-12): _
```

Just pick a number and press enter.

---

### Command-Line Mode (For Scripts & Automation)

Use direct commands for automation or if you prefer typing commands:

#### First time setup
```bash
# Auto-install everything (recommended!)
sudo xray-cli install-everything

# Or, get your vless:// config
xray-cli get-config "vless://your-config-here"

# Or from a subscription URL
xray-cli get-config "https://provider.com/api/subscription/token"

# Check status
xray-cli status
```

#### Start proxy
```bash
sudo xray-cli proxy start
```

#### Stop proxy
```bash
sudo xray-cli proxy stop
```

#### Restart proxy
```bash
sudo xray-cli proxy restart
```

#### Enable system-wide routing (TUN mode)
```bash
sudo xray-cli tun start
```

#### Disable TUN mode
```bash
sudo xray-cli tun stop
```

#### Enable autostart on boot (Xray, and TUN if enabled)
```bash
sudo xray-cli autostart enable
```

#### Disable autostart
```bash
sudo xray-cli autostart disable
```

#### Check autostart status
```bash
xray-cli autostart status
```

#### Run specific app with proxy
```bash
xray-cli run firefox
xray-cli run chromium --incognito
```

#### Check status
```bash
xray-cli status
```

Output:
```
==================================================
🔍 Xray CLI Status
==================================================
✓ ✨ Config found: 1.2.3.4:443
✓ ✨ Xray proxy: Running 🚀 (SOCKS5 on 127.0.0.1:1080)
✓ ✨ Redsocks: Running 🔄
✓ ✨ TUN mode: Enabled 🛡️ (all traffic routed)
✓ ✨ Autostart: Enabled 🔄 (starts on boot)
==================================================
```

## Commands Reference

```
xray-cli                              # Interactive menu
sudo xray-cli install-everything      # Auto-install Xray, Redsocks & config
xray-cli get-config <url>             # Save vless:// config
xray-cli status                       # Show status
sudo xray-cli proxy start             # Start proxy
sudo xray-cli proxy stop              # Stop proxy
sudo xray-cli proxy restart           # Restart proxy
sudo xray-cli tun start               # Enable TUN mode
sudo xray-cli tun stop                # Disable TUN mode
sudo xray-cli autostart enable        # Enable autostart on boot
sudo xray-cli autostart disable       # Disable autostart
xray-cli autostart status             # Check autostart status
xray-cli run <app> [args]             # Run app with proxy
```

## Examples

### Quick Start (Interactive)
```bash
# 1. Run interactive menu with sudo
sudo xray-cli

# 2. Choose option 11 (Install Everything)
# 3. Choose option 6 (Get/Update Config)
# 4. Paste your vless:// URL
# 5. Choose option 2 (Start Proxy)
# 6. (Optional) Choose option 4 (Enable TUN Mode)
# 7. (Optional) Choose option 9 (Enable Autostart)
# 8. Done! ✓
```

### Quick Start (Command-Line)
```bash
# 1. Auto-install everything (recommended!)
sudo xray-cli install-everything

# 2. Get config
xray-cli get-config "vless://abc@server.com:443?security=reality&pbk=key"

# 3. Start proxy
sudo xray-cli proxy start

# 4. Enable system-wide routing (optional)
sudo xray-cli tun start

# 5. Enable autostart (optional, remembers TUN mode preference)
sudo xray-cli autostart enable

# 6. Check it's working
xray-cli status
```

### Run Specific Apps with Proxy
```bash
# Firefox
xray-cli run firefox

# Chromium in incognito
xray-cli run chromium --incognito

# Any app
xray-cli run <app-name>
```

### Stop Everything
```bash
sudo xray-cli tun stop
sudo xray-cli proxy stop
```

## How It Works

1. **Xray** creates a SOCKS5 proxy on `127.0.0.1:1080`
2. **Your apps** connect to this local proxy
3. **Xray encrypts** traffic using VLESS protocol with Reality
4. **Traffic looks like normal HTTPS** (bypasses censorship!)
5. **TUN mode (optional)** routes ALL system traffic through the proxy
6. **Autostart** uses a systemd service to launch Xray (and Redsocks/TUN) on boot, remembering your last TUN mode preference.

## Troubleshooting

### "Xray not found"
Install Xray first:
```bash
sudo bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```
Or use the new auto-setup: `sudo xray-cli install-everything`

### "Redsocks not found"
Install redsocks:
```bash
yay -S redsocks  # Arch
sudo apt install redsocks  # Ubuntu/Debian
```
Or use the new auto-setup: `sudo xray-cli install-everything`

### "Config not found"
Run the get-config command first:
```bash
xray-cli get-config "vless://..."
```

### Check if proxy is working
```bash
# Check status
xray-cli status

# Test with curl
curl --proxy socks5://127.0.0.1:1080 https://ipinfo.io
```

### Proxy won't start
```bash
# Check if xray is already running
ps aux | grep xray

# Kill old processes
sudo pkill xray

# Try again
sudo xray-cli proxy start
```

### Autostart not working
```bash
# Check if the service file exists
ls /etc/systemd/system/xray-cli.service

# Check service status
systemctl status xray-cli.service

# Try re-enabling autostart
sudo xray-cli autostart enable
```

## Configuration Files

- `~/.config/xray-cli/config.json` - Your parsed vless config
- `~/.config/xray-cli/xray.json` - Generated Xray config
- `/etc/redsocks.conf` - Redsocks configuration

## Security Notes

🛡️ **Your UUID is like a password** - keep your vless:// URL private!

🔒 **Reality Protocol** - Makes your traffic look like normal HTTPS browsing, designed to bypass Deep Packet Inspection (DPI) in restrictive countries.

## Notes

This tool was created with AI assistance (Claude) to simplify Xray proxy management. The code is open source and available for anyone to use, modify, or learn from. **The new "Install Everything" feature and enhanced autostart capabilities significantly improve ease of use and persistence.**

## License

MIT

## Contributing

Found a bug? Open an issue or submit a PR.

## Support

For issues and questions:
- Check the [Troubleshooting](#troubleshooting) section
- Open an issue on GitHub
- Read Xray documentation: https://xtls.github.io/
