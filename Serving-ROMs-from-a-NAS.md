This process requires [access to the Lakka commandline](http://www.lakka.tv/doc/Accessing-Lakka-command-line-interface/) and is also only recommended for those comfortable working in a Linux shell environment.

## Mounting a Windows/CIFS/Samba share

Create the mount point folder:

    mkdir /storage/roms/nas

Create the mount unit:

    nano /storage/.config/system.d/storage-roms-nas.mount

Save and exit: `CTRL+O` then `Enter` to save, then `CTRL+X` to exit

**Note:** The file name of the mount unit must match the path to the mount point (slashes are replaced with dashes, as in the above example - mount point: `/storage/roms/nas` -> unit file name: `storage-roms-nas.mount`)

Add this content, replacing placeholders with your IP, username and password information:

    [Unit]
    Description=cifs mount script
    Requires=network-online.service
    After=network-online.service
    Before=retroarch.service

    [Mount]
    What=//192.168.0.31/roms
    Where=/storage/roms/nas
    Options=username=myusername,password=mypassword,rw
    Type=cifs
    
    [Install]
    WantedBy=multi-user.target

**Note:** If the server does not support samba version 2 or higher, you have to add `vers=1` to the `Options` line:

    ...
    Options=username=myusername,password=mypassword,rw,vers=1
    ...

Enable and start the service:

    systemctl enable storage-roms-nas.mount
    systemctl start storage-roms-nas.mount

If the mount was successful, the volume will be mounted automatically from now on at boot.

## Mounting an NFS share

NFS works exactly the same, except you have to use:

    What=192.168.0.31:/roms
    Type=nfs