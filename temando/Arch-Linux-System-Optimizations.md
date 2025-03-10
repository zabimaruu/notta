[Go Back](https://rmelendez.net)

## Bios/Firmware Updates
- [**Fwupd**](https://wiki.archlinux.org/title/Fwupd) - simple daemon to allow session software to update device firmware on your local machine. It's designed for desktops, but also usable on phones and headless servers
- 
### Power Saving Tools (Mostly Laptops)

- [**TLP**](https://wiki.archlinux.org/title/TLP) - is a feature-rich command line utility for Linux, **saving laptop battery power** without the need to delve deeper into technical details

**Arch Installation**
```bash
sudo pacman -S tlp

#Enable TLP service
sudo systemctl enable tlp.service

#Start using the service right away (no need to reboot)
sudo systemctl start tlp.service

# Also it is a good idea to mask the service by running
sudo systemctl mask systemd-rfkill.service
sudo systemctl mask systemd-rfkill.socket
```

- [**Tlp-rdw**](https://archlinux.org/packages/?name=tlp-rdw) - When using the Radio Device Wizard, install **tlp-rdw** it is required to use [**NetworkManager**](https://wiki.archlinux.org/title/NetworkManager) and enable it by running

```bash
sudo systemctl enable NetworkManager-dispatcher.service
```

There are also some **Front end** apps that can be installed to configure **TLP** check the [**Arch Wiki TLP Page**](https://wiki.archlinux.org/title/TLP) for more details

- [**Auto-CPUFreq**](https://github.com/AdnanHodzic/auto-cpufreq) - Automatic CPU speed & power optimizer for Linux
	- *NOTE: Never combine **TLP** with **Auto-CPUFreq** only use one at the time, not both*
