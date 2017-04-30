## ROMS

The required format for the CD images is BIN+CUE.

If the CUE is missing, you can create it like this:

    FILE "NameOfTheBin.bin" BINARY
      TRACK 01 MODE2/2352
        INDEX 01 00:00:00

We recommand CD images from [Redump](http://redump.org).

## BIOSes

You will need 3 BIOSes:

| MD5SUM                           | Name         |
|----------------------------------|--------------|
| 8dd7d5296a650fac7319bce665a6a53c | scph5500.bin |
| 490f666e1afb15b7362b406ed1cea246 | scph5501.bin (Can be renamed from scph7003.bin) |
| 32736f17079d0b2b7024407c39bd3050 | scph5502.bin |