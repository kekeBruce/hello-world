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

## desktop setup
### flat theme and icon
install `unity-tweak-tool` `flatabulous-theme` `ultra-flat-icons`

### font
chinese font 文泉驛微米黑  
install `fonts-wqy-microhei `

### Dock
install `cairo-dock`
http://github.com - automatic!
[GitHub](http://github.com)
