**You should never blindly execute scripts from unreliable sources (which this repository is). Familiarize yourself with the script content before you launch anything.**

To make a script executable:

```
 $ chmod +x <scriptname>
```

## mkarchusb

Creates Arch Linux live USB drive for installation or rescue purposes. It is a simple wrapper of **mkarchiso** utility from [archiso](https://archlinux.org/packages/?name=archiso) package, which is used to build official [monthly images](https://archlinux.org/download/).

Usage:

```
# mkarchusb <disk>
```

**mkarchusb** takes a single _disk_ argument (where your flash drive is, in the form of _/dev/sdx_), unmounts it, makes **mkarchiso** build an ISO with the default **releng** profile, writes it into the _disk_ and removes all temporary files. It would only work on Arch Linux or at least on any distribution with pacman installed and properly configured, as **mkarchiso** relies on pacman to get all the files for the image. Naturally you would need fast internet connection (or a lot of patience) and sufficient amount of space on `/tmp` (around 4 GB), as this is where **mkarchusb** puts a temporary working directory.
