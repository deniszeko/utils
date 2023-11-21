**You should never blindly execute scripts from unreliable sources (which this repository is). Familiarize yourself with the script content before you launch anything.**

To make a script executable:

```
$ chmod +x <scriptname>
```

## automode

Automatically switches between light and dark modes (aka schemes or styles) of GNOME 45+. Uses systemd timers which are triggered daily on sunrise and sunset.

**Requirements:**
- Internet connection to update sunrise/sunset times through the year.
- [jq](https://github.com/jqlang/jq) package installed. Needed to parse JSON web API response.
- Enabled geolocation in GNOME Settings > Privacy > Location Services. Strictly speaking you can enable it just once prior to installation to populate initial coordinates, and then keep it disabled if your device is stationary.

**Installation:**

```
$ automode
```

Execute the script _without_ root privileges. It writes, enables and starts two _user_ systemd timers (for sunrise and sunset events) with two corresponding static services (to enable light and dark modes), then copies itself into the `~/.local/bin` directory. You can delete a script afterwards. When either timer is triggered, first service switches DE mode, then a script in `~/.local/bin` is executed to get new sunrise/sunset times from https://sunrise-sunset.org/api, edit timers accordingly and reload them.

**Uninstallation:**

```
$ rm ~/.local/bin/automode ~/.config/systemd/user/autolight.timer ~/.config/systemd/user/autolight.service ~/.config/systemd/user/autodark.timer ~/.config/systemd/user/autodark.service
$ systemctl --user daemon-reload
```

## mkarchusb

Creates Arch Linux live USB drive for installation or rescue purposes. It is a simple wrapper of **mkarchiso** utility from [archiso](https://archlinux.org/packages/?name=archiso) package, which is used to build official [monthly images](https://archlinux.org/download/).

**Usage:**

```
# mkarchusb <disk>
```

**mkarchusb** takes a single _disk_ argument (where your flash drive is, in the form of _/dev/sdx_), unmounts it, makes **mkarchiso** build an ISO with the default **releng** profile, writes it into the _disk_ and removes all temporary files. It would only work on Arch Linux or at least on any distribution with pacman installed and properly configured, as **mkarchiso** relies on pacman to get all the files for the image. Naturally you would need fast internet connection (or a lot of patience) and sufficient amount of space on `/tmp` (around 4 GB), as this is where **mkarchusb** puts a temporary working directory.
