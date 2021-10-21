Accessing Lakka command line interface is useful if you want to debug the system, or if you need to edit the configuration file manually. It is for advanced users only. For begginners, using the graphical interface should be enough.

There are 3 ways to access the command line interface:

 * SSH
 * Direct access with a keyboard
 * Serial

## SSH

The easiest way to configure Lakka is to connect it via SSH. SSH is a service running on your Lakka box, it lets you run commands on your box, such as editing configuration files.

To access your Lakka box through SSH, you need to connect your Lakka device to the network.

Then, you have to enable SSH in **Settings->Services**.

You will need an SSH client to connect to your box. You will also need to [know the IP address of your Lakka box](Finding-the-IP-of-your-Lakka-box).

### On Linux or Mac OS X

If you're using Linux or Mac OS X, there is already an SSH client on your system. Just open a terminal, and type this command:

    ssh root@ip-of-your-box

SSH will then ask for your password, the default password is **root**.

### On Windows

On Windows, you will need an SSH client like [Putty](https://www.putty.org/)

Use putty to connect your Lakka box, enter the IP of your box in the hostname field, set SSH connection type. The username is **root** and the password is also **root**.

## Direct access

You will need to edit the cmdline passed to the kernel by the bootloader, in order to enable the **console service** and disable the **retroarch service**. You will also need to plug a keyboard to type any commands.

### Editing the cmdline

You have to ensure that these options are present in the [cmdline](The-bootloader):

    textmode retroarch=0

 * `textmode` will enable the console service
 * `retroarch=0` will disable the retroarch service

### Booting to console

Once the system is booting, you will not see RetroArch launching. It's normal, since we disabled retroarch service. AFter the boot process is complete, you will see shell prompt. Execute `systemctl start retroarch.target` to make sure that all services/mounts needed for RetroArch (the UI) are running, especially the overlayfs mounts in `/tmp` (use `mount` or `df -h` to see available mounts).

## Serial

On the development boards, using an USB to TTL cable can give you access to the serial console. The advantage of using this interface is that you can get the logs of the bootloader and the early kernel logs. It is useful if you plan to port Lakka to a new hardware.

TODO
