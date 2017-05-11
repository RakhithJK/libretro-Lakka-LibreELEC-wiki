This adapter requires the use of a userspace driver.

You can start it in SSH:

    systemctl start wii-u-gc-adapter

And to auto start it on every boot:

    systemctl enable wii-u-gc-adapter

Note: This driver is not compatible with old kernels