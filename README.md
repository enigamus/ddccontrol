### The changes are minor
* no more warning at startup using gddccontrol if the generic profile (basic, not by manufacturer) is used, thus less annoying if otherwise the use is possible

### Installation from source: Arch Linux
```shell
# AUR remove : ddccontrol ddc control-git
# AUR install : ddccontrol-db-git
sudo pacman -S autoconf automake git intltool libxml2 pciutils
git clone https://github.com/enigamus/ddccontrol.git
cd ddccontrol
./autogen.sh
./configure --prefix=/usr --sysconfdir=/etc
make
sudo make install
```
---

# DDC/CI control

DDCcontrol is a software used to control monitor parameters, like brightness, contrast, RGB color levels and others.

DDCcontrol consists of:

* `ddccontrol` - command-line tool for monitor parameters control
* `gddccontrol` - GUI tool for monitor parameters control

## Installation

The most convenient way to install DDCcontrol is to use packages from official distribution repositories.

Manual installation is more complicated, but contains latest version of software and more monitor profiles.

### Installation from official packages

DDCcontrol tools, `ddccontrol` and `gddccontrol` can be installed from official distribution repositories with following command:

* on Ubuntu/Debian: `sudo apt install ddccontrol gddccontrol ddccontrol-db i2c-tools`
* on Fedora: `sudo dnf install ddccontrol ddccontrol-gtk`
* on openSUSE: `sudo zypper in ddccontrol`

You might need to restart your system after installing `i2c-tools`.

### Installation from sources

Install build dependencies:

* on Ubuntu: `sudo apt install intltool i2c-tools libxml2-dev libpci-dev libgtk2.0-dev liblzma-dev`
* on Solus: `sudo eopkg install -c system.devel`  
 `sudo eopkg install autoconf automake intltool i2c-tools m4 diffutils libtool-devel xz-devel pciutils-devel libxml2-devel libgtk-2-devel`
* on others: `TODO`

Clone, build and install built version:

```shell
git clone https://github.com/ddccontrol/ddccontrol.git
cd ddccontrol
./autogen.sh
./configure --prefix=/usr/ --sysconfdir=/etc --libexecdir=/usr/lib
make
sudo make install
```

Monitor database is required for proper functionality. See for [ddccontrol-db installation](https://github.com/ddccontrol/ddccontrol-db#installation).

## Usage

### From GUI using gddccontrol

`gddccontrol` is a graphical utility for monitor configuration. It is called **Monitor Settings** in list of applications.

Following configuration is needed to allow non-root user to use `gddccontrol`:

```shell
sudo adduser $USER i2c
sudo /bin/sh -c 'echo i2c-dev >> /etc/modules'
```

Utility can launched directly from commandline:

```shell
sudo gddccontrol
```

### From command line using ddccontrol

`ddccontrol` allows monitor configuration directly from commandline. To probe I2C devices to find monitor buses use:

```shell
sudo ddccontrol -p
```

To read value of control `0x10` (brightness on VESA compliant monitors) for device `dev:/dev/i2c-4`:

```shell
sudo ddccontrol -r 0x10 dev:/dev/i2c-4
```

To set value of control `0x10` (brightness on VESA compliant monitors) to `75` for device `dev:/dev/i2c-4`:

```shell
sudo ddccontrol -r 0x10 -w 75 dev:/dev/i2c-4
```

See `ddccontrol -h` for more information.

## License

The project is licensed under `GNU General Public License v2.0` license. See [COPYING](COPYING) for details.
