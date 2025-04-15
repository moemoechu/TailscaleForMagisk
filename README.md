# Tailscale for Magisk

[![GitHub Release](https://img.shields.io/github/v/release/moemoechu/TailscaleForMagisk)](https://github.com/moemoechu/TailscaleForMagisk/releases)
[![GitHub Download](https://img.shields.io/github/downloads/moemoechu/TailscaleForMagisk/total)](https://github.com/moemoechu/TailscaleForMagisk/releases)

The project is a [Magisk](https://github.com/topjohnwu/Magisk) module for Tailscale, Support Magisk and KernelSU

# Disclaimer

The project is not responsible for bricked equipment, damaged SD cards, or burned SoC

# Install

Download zip in release and flash using Magisk Manager or MMRL.

# Usage

After the module is installed, it runs in the background

## Base usage

Executable file `tailscale-sv`、`tailscaled`、`tailscale` will copy to `/system/bin`, you can directly run command in root shell

```bash
tailscale-sv status
already logged in,management address:http://localhost:8088,check the status excute`tailscale status` by terminal
```

## Control tailscaled service

Start, restart, stop tailscaled service

```
tailscale-sv start
tailscale-sv restart
tailscale-sv stop
```

## Login in tailscale

- Direct access to the web administration page: http://localhost:8088

- ```
    # Executive command
    tailscale login
  ```
  tailscale data will storage in /data/adb/tailscale

## Magic DNS

If you want to use tailscale's magic DNS, some additional config must be apply

### With Termux

```bash
vim $PREFIX/etc/resolv.conf
# add nameserver 100.100.100.100 on top
```

```
nameserver 100.100.100.100
search your-magicdns.ts.net
```

### With chroot

```bash
vim /etc/resolv.conf
# add nameserver 100.100.100.100 on top
```

```
nameserver 100.100.100.100
search your-magicdns.ts.net
```

### With clash

You must using full dns name like `node.your-magicdns.ts.net`

```yaml
# add follow config
dns:
  nameserver-policy:
    "+.ts.net": "100.100.100.100"
```

# Uninstall

- Uninstall this module from the Magisk Manager application，will delete `/data/adb/service.d/tailscale_service.sh`，Reserved data directory `/data/adb/tailscale`

- You can use commands to clear data: `rm -rf /data/adb/tailscale`
