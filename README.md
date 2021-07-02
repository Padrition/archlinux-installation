# archlinux-installation
My Arch Linux installation guide for my personal needs, but feel free to use it 

## ISO download

[Link](https://distrowatch.com/dwres/torrents/archlabs-2020.11.04-x86_64.iso.torrent) to DistroWatch's archlabs-linux torrent.

## Drivers

* [rtl8821ce](https://github.com/tomaspinho/rtl8821ce) Wifi driver

```
git clone https://github.com/tomaspinho/rtl8821ce.git

cd rtl8821ce

sudo ./dkms-install.sh
```

* Nvidia

The following taken from [lutris wiki page](https://github.com/lutris/docs/blob/master/InstallingDrivers.md):
First, enable multilib.

To enable multilib repository, uncomment the `[multilib]` section in `/etc/pacman.conf`

<pre style="margin-bottom: 0; border-bottom:none; padding-bottom:0.8em;">/etc/pacman.conf
--------------------------------------------------------------------------------------
[multilib]
Include = /etc/pacman.d/mirrorlist</pre>

Then upgrade the system `sudo pacman -Syu`.

### Nvidia:

_**Warning**: Please ensure your graphics card is supported by modern Nvidia driver before installing._
_For a list of supported GPUs click here: https://www.nvidia.com/Download/driverResults.aspx/149138/en-us_

Proprietary driver and support for Vulkan are required for proper functionality of games.

To install it, execute following command:

    sudo pacman -S nvidia-dkms nvidia-utils lib32-nvidia-utils nvidia-settings vulkan-icd-loader lib32-vulkan-icd-loader
    
    
## Trubleshooting 

* Backlight don't changing 

Set a kernel parametr ```acpi_backlight``` to ```video```

Use [this solution](https://unix.stackexchange.com/a/322862) .
