[Go Back](https://rmelendez.net)


## GPU Pass Through
1. **Add IOMMU Support**
	1. `nano /etc/default/grub`
	2. For Intel 
		1. `"GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on"`
	3. For AMD
		1. `"GRUB_CMDLINE_LINUX_DEFAULT="quiet amd_iommu=on"`
	4. Run `update-grub`
	5. Reboot machine/server
2. **Check IOMMU Support is enabled**
	1. Run `dmesg | grep -e DMAR -e IOMMU`
		1. There should be a line that looks like `"DMAR: IOMMU enabled"`. If there is no output, something is wrong
3. **Add VFIO Modules**
	1. `nano /etc/modules`
		1. `vfio`
		2. `vfio_iommu_type1`
		3. `vfio_pci`
	2. Save file and close
4. **Find GPU PCI Identifier**
	1. Run `lspci`
	2. Copy the HEX values from your GPU and Run the following (Replace the ####.####,####.####) for the actual values
	3. `echo "options vfio-pci ids=####.####,####.#### disable_vga=1"> /etc/modprobe.d/vfio.conf`
	4. Reboot machine/server

## Windows GPU Pass Through Drivers & Tricks
1. [Parsec](https://parsec.app/) - Application to remote into PC and Play games as well (Client only available on MacOS and Windows)
	1. For Linux enable RDP and use **Renmina**
2. Install [VB-Audio Virtual Driver](https://vb-audio.com/Cable/index.htm) to have audio enabled within the VM
