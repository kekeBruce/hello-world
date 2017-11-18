# Ubuntu 14.04 setup

platform : Acer E5-473G-56cs

## boot manager issue

the boot manager grub is always no showing, no matter what setting in windows
8.1  

**solution**: Because the acer ufei is not recognize the secure boot
certification  
automatically,manual setting is needed:

according to [this](https://askubuntu.com/questions/771455/dual-boot-ubuntu-with-windows-on-acer-aspire/771749#771749):


    Press F2 to enter into BIOS and do following:

    *   Set supervisor password from Security menu option.

    *   Set BootMode to 'UEFI' from Boot menu option.

    *   Enable SecureBoot from Boot menu option.

    *   From Security menu option - Select 'UEFI file as trusted for
        executing' press Enter then 'HDD0' appears press Enter then 'EFI'
        appears press Enter then select 'ubuntu' option from the list (only
        listed if you have ubuntu installed already) press Enter then choose  
        'shimx64.efi' (In my case it's the third entry) press Enter give it  
        a name and press Enter.

    *   Go back to Boot menu option and under Boot priority goto
        'ubuntu' item in the list and press F6 until it become top most item  
        in the list. Repeat same for 'Windows Boot manager' until it becomes  
        second top most item in the list.

    Press F10 to save changes and exit.

And then press F12 enter boot Menu and select the name you set upon,  
enter the grub. done
***
## desktop setup
### flat theme and icon
install `unity-tweak-tool` `flatabulous-theme` `ultra-flat-icons`

### font
chinese font 文泉驛微米黑  
install `fonts-wqy-microhei `

### Dock
install `cairo-dock`
***

## Wifi issue  

**quip**: Qualcomm Atheros QCA9337 wifi

wifi is not working because there is no driver in that.

`$ lspci // 03:00.0 Network controller: Qualcomm Atheros Device 0042 (rev 30)`

`$ ifconfig` there is no wifi interface

    docker0   Link encap:Ethernet  HWaddr 56:84:7a:fe:97:99  
              inet addr:172.17.42.1  Bcast:0.0.0.0  Mask:255.255.0.0
              UP BROADCAST MULTICAST  MTU:1500  Metric:1
              RX packets:0 errors:0 dropped:0 overruns:0 frame:0
              TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:1000
              RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

    eth0      Link encap:Ethernet  HWaddr f0:76:1c:bf:14:02  
              inet addr:192.168.1.102  Bcast:192.168.1.255  Mask:255.255.255.0
              inet6 addr: fe80::f276:1cff:febf:1402/64 Scope:Link
              UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
              RX packets:75 errors:0 dropped:0 overruns:0 frame:0
              TX packets:322 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:1000
              RX bytes:11973 (11.9 KB)  TX bytes:66200 (66.2 KB)

    lo        Link encap:Local Loopback  
              inet addr:127.0.0.1  Mask:255.0.0.0
              inet6 addr: ::1/128 Scope:Host
              UP LOOPBACK RUNNING  MTU:65536  Metric:1
              RX packets:92 errors:0 dropped:0 overruns:0 frame:0
              TX packets:92 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:1
              RX bytes:7100 (7.1 KB)  TX bytes:7100 (7.1 KB)


### steps

1. install
[driver](https://www.kernel.org/pub/linux/kernel/projects/backports/stable/v4.4.2/)  
sudo apt-get install build-essential linux-headers-generic  
wget https://www.kernel.org/pub/linux/kernel/projects/backports/stable/v4.4.2/backports-4.4.2-1.tar.xz
tar xvfj backports-4.4.2-1.tar.xz  
cd backports-4.4.2-1  
make defconfig-ath10k  
make  
sudo make install  
/\**reboot here*\*/

2. [firmware](https://github.com/ajaybhatia/Qualcomm-Atheros-QCA9377-Wifi-Linux.git)
replace/create the file in `/lib/firmware/atk10k/QCA9337/hw1.0/` with `Qualcomm-Atheros-QCA9377-Wifi-Linux/firmware-only/*`
/\**reboot here*\*/

done
