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

* Keyboard layout switching

put in ```/usr/share/X11/xorg.conf.d/00-keyboard.conf```

```
Section "InputClass"
    Identifier "system-keyboard"
    MatchIsKeyboard "on"
    Option "XkbLayout" "us,ru"
    Option "XkbModel" "pc102"
    Option "XkbOptions" "grp:alt_shift_toggle"
EndSection
```
* Screen tearing

put in ```/usr/share/X11/xorg.conf.d/10-nvidia.conf```

```
Section "Screen"
    Identifier  "Screen0"
    Device      "Device0"
    Monitor     "Monitor0"
    Option      "MetaModes" "nvidia-auto-select +0+0 {ForceFullCompositionPipeline=On}"
    Option      "AllowIndirectGLXProtocol" "off"
    Option      "TripleBuffer" "on"
EndSection
```
* Kernel freez becouse of wifi drivers

solution provided by Ari Archer

```
[Forwarded from Ari Archer]
1. add this to /var/lib/NetworkManager/NetworkManager-intern.conf
[connectivity]
.set.enabled=false

2.add this to /etc/modprobe.d/blacklist.conf
blacklist rtw88_8821ce

3. type
sudo reboot -f
3.1. boot up, log in, wait a few seconds and type
shutdown now
3.2. wait a couple of seconds and boot up
3.3. check if everything worked with
sudo lsmod | grep -i rtw
(should get no output if everything went good)
3.4. reinstall the driver from  https://github.com/tomaspinho/rtl8821ce if still happens
```
