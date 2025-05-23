# System Administration Final Project

## Base Installation
The first step is to download the appropriate installation image for the appropriate architecture and storage medium for your server environment and flash it. Once you have booted into the install select to open a shell.
![](bsd-setup/1.png)
Type the command 'geom disk list' to get a list of the disks available. Find the disk you plan to install on and type 'dd if=/dev/urandom of=/dev/[DRIVE NAME] bs=1M status=progress' This will randomize our disk, making it more difficult for an attacker to discern things.
![](bsd-setup/2.png)
Deselect the various additional components as we you will not need them. (Unless you intend to run Wine on your server, in which case, you should keep lib32.)
![](bsd-setup/3.png)
Encrypt the disk, and encrypt the swap. In our case, we opt for the default 'stripe' option on the next page as we are using SLED and not RAID, but your circumstances may differ.
![](bsd-setup/4.png)
As we intend to have a server that is openly facing the internet, we will want to make sure that our time is in sync.
![](bsd-setup/5.png)
Enable all system hardening measures except for 'syslogd,' for remote logging. 
![](bsd-setup/6.png)
When prompted to add users select 'yes.'
![](bsd-setup/7.png)
Be sure to add your user to both the wheel and video groups.
![](bsd-setup/8.png)
## Graphical and User Interface
Install the following list of packages. These are intended just as a base set of user applications which can enable a usable experience.
![](bsd-setup/9.png)
Enable 'seatd' as it will be required by sway. Vi into '/usr/local/etc/doas.conf'
![](bsd-setup/10.png)
Type 'i' to enter instertion mode. Then type the following. Hit the 'Esc' key to exit insertion mode. Then type ':wq + Enter' to save the file.
![](bsd-setup/11.png)
Now, as your regular user type 'chsh'
![](bsd-setup/12.png)
Use your arrow key to move down to the line containing your shell (aka '/bin/sh') and type 'x' until that portion goes away. Then type 'i' to enter insertion mode just like we did above and put in the following path to your new shell. Write and exit.
![](bsd-setup/13.png)
Clone, copy over, and delete your dotfiles configuration.
![](bsd-setup/14.png)
Now, when you reboot the machine using 'doas reboot', you will login to your new ZSH configuration, and seatd will be running.
![](bsd-setup/15.png)
Now, you can enter sway by simply typing 'sway'
![](bsd-setup/16.png)
## Web Server and Firewall
This would be a good time to install the web server and firewall of your choice. Personally, I am partial to NGINX, but decided to use Apache for this demo.
## Snort
## A little caveat
Just as a little note here, the FreeBSD installation which I had spun up in the first part is running on VMWare, and I am unable to make any configuration changes nor install any graphics drivers that allow Wayland to actually function properly on this platform, though most people should almost never run into this situation when running either on real world hardware or an alternative virtual machine environment (I recommend 'libvirt' and 'virt-manager', personally.) All of that is to say that the rest of this was completed on a Linux Mint VM.

Start by installing snort through your package manager.

![](snort/0.png)

Then clone the GitHub repository for the GUI.

![](snort/1.png)

'cd' into the sub-directory containing the installer. 'chmod' it to give it executable permissions and run it.

![](snort/2.png)

After entering the main application, open the rules generator. The only thing we need to do for this simple demo is to set the following settings on the blue space at the top. Opt to create an alert for both denial-of-service as well as attempted-dos.

![](snort/4.png)

Here I have a webpage opened in the background to my Apache server homepage. And I am choosing to run Snort for 6 minutes. 

![](snort/5.png)

Finally, I run the exploit script and open the log analyzer after it completes...

![](snort/6.png)
