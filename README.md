# [Battery Monitor]( https://hsbasu.github.io/battery-monitor)

<p align="center">
	<img src="https://raw.githubusercontent.com/hsbasu/battery-monitor/master/usr/share/icons/hicolor/scalable/apps/battery-monitor.svg?sanitize=true" height="64">
</p>

[![License](https://img.shields.io/github/license/hsbasu/battery-monitor?label=License)](https://github.com/hsbasu/battery-monitor/blob/master/LICENSE)
![GitHub repo size](https://img.shields.io/github/repo-size/hsbasu/battery-monitor?label=Repo%20size)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/hsbasu/battery-monitor?label=Latest%20Stable%20Release)](https://github.com/hsbasu/battery-monitor/releases/latest)

[![Downloads](https://img.shields.io/github/downloads/hsbasu/battery-monitor/total?label=Downloads&style=flat-square)](#download-latest-version)
[![GitHub release (latest by date and asset)](https://img.shields.io/github/downloads/hsbasu/battery-monitor/1.0.2/battery-monitor_1.0.2_all.deb?color=blue&label=Downloads%40Latest)](https://github.com/hsbasu/battery-monitor/releases/download/1.0.2/battery-monitor_1.0.2_all.deb)

Many a times we forget to remove the laptop charger. This can reduce the battery life significantly due to overcharging. This is where Battery Monitor comes into play.

Battery Monitor is a utility tool developed on Python3 and PyGtk3. It will notify the user about charging, discharging, not charging and critically low state of the battery on Linux (surely if the battery is present). Along with showing the notification repetitively, It also plays a sound so that you don't miss the notification.

## Download Latest Version

[Download Source [.zip]](https://github.com/hsbasu/battery-monitor/archive/refs/tags/1.0.2.zip)

[Download Source[.tar.gz]](https://github.com/hsbasu/battery-monitor/archive/refs/tags/1.0.2.tar.gz)

[Download Binary[.deb]](https://github.com/hsbasu/battery-monitor/releases/download/1.0.2/battery-monitor_1.0.2_all.deb)

## Features and Screenshots
Battery Monitor notifies the user:
1. Whether [battery is present](#initial-state),
2. When charger is [plugged in](#charging-state),
3. When charger is [unplugged](#discharging-state),
4. When battery is [full and charger is not unplugged](#not-charging-state),
5. When battery is [critically low](#critically-low-battery-state).

Additionally, it can show notifications:
1. At three user-defined battery percentage during discharging,
2. At one user-defined battery percentage during charging,
3. Along with playing a sound (Mute option is not available yet).

#### Initial State

![Initial State](https://github.com/hsbasu/battery-monitor/raw/gh-pages/screenshots/initial-state.png)

#### Charging State

![Charging State](https://github.com/hsbasu/battery-monitor/raw/gh-pages/screenshots/charging.png)

#### Discharging State

![Discharging State](https://github.com/hsbasu/battery-monitor/raw/gh-pages/screenshots/discharging.png)

#### Not Charging State

![Not Charging State](https://github.com/hsbasu/battery-monitor/raw/gh-pages/screenshots/not-charging.png)

#### Critically Low Battery State

![Critically Low Battery State](https://github.com/hsbasu/battery-monitor/raw/gh-pages/screenshots/critically-low.png)

### Settings Window
In Settings menu, you can configure and adjust settings for Battery Monitor. Here, you can set the battery percentage levels at which you want to get notifications. The warning levels are listed in ascending order. **Critical Battery Warning** refers to the lowest level while **First Custom Warning** refers to the highest level. Custom warning levels are optional.

**N.B.** If you change any configuration, it will be in action only after next reboot.

![Battery Monitor GUI](https://github.com/hsbasu/battery-monitor/raw/gh-pages/screenshots/settings-window.png)

## Contents
- [Download Latest Version](#download-latest-version)
- [Features and Screenshots](#features-and-screenshots)
- [Dependencies](#dependencies)
	- [Debian/Ubuntu based systems](#debianubuntu-based-distro)
	- [Other Linux-based systems](#other-linux-based-distro)
- [Installation](#build-and-install-the-latest-version)
	- [Debian/Ubuntu based systems](#debianubuntu-based-systems)
	- [Other Linux-based systems](#other-linux-based-systems)
	- [For Developers](#for-developers)
- [User Manual](#user-manual)
	- [Auto Start](#auto-start)
- [Issue Tracking and Contributing](#issue-tracking-and-contributing)
- [Contributors](#contributors)

## Dependencies
```
acpi
python3
python3-gi
python3-setuptools
libnotify4
libappindicator3-1
gir1.2-appindicator3-0.1
```
To use or test **Battery Monitor**, you need these dependencies to be installed.

### Debian/Ubuntu based distro
To install dependencies on Debian/Ubuntu based systems, run:
```
sudo apt install acpi python3 python3-gi python3-setuptools \
libnotify4 libappindicator3-1 gir1.2-appindicator3-0.1
```
**Note**: If you are using `gdebi` to install **Battery Monitor** from a `.deb` file, it will auto matically install the dependencies and you can skip this step.

### Other Linux-based distro
Remove `apt install` in the command given in [Debian/Ubuntu based distros](#debianubuntu-based-distro) and use the command for the package manager of the target system(eg. `yum install`, `dnf install`, `pacman -S` etc.)

**Note**: There might be cases where one or more dependencies might not be available for your system. But that is highly unlikely. In such situations, please [create an issue](#issue-tracking-and-contributing).

## Build and Install the Latest Version

### Debian/Ubuntu based systems
There are two methods, this app can be installed/used on a Debian/Ubuntu based system. First, download and unzip the source package using:
```
wget https://github.com/hsbasu/battery-monitor/archive/refs/heads/master.zip
unzip master.zip
cd battery-monitor-master
```
1. **Option 1:** Manually copying necessary files to root (`/`). For that, follow the steps below:
	1. [**Optional**] To make translations/locales in languages other than **English**, run:
		```
		make
		```
	from the `/path/to/repo` in a terminal. It will create the translations/locales in `usr/share/locale`.
		
	2. Copy the contents of `usr/` to `/usr/`:
		```
		sudo cp -R usr /
		```
	3. Copy the contents of `etc/` to `/etc/`:
		```
		sudo cp -R etc /
		```
	4. Compile `schemas` using:
		```
		sudo glib-compile-schemas /usr/share/glib-2.0/schemas
		```
	5. Run `battery-monitor` from terminal or use the `battery-monitor.desktop`.
	
2. **Option 2:** Build a debian package and install it. To build a debian package on your own:
	1. After using `cd battery-monitor-master`, run:
		```
		dpkg-buildpackage --no-sign
		```
	This will create a `battery-monitor_*.deb` package at `../  battery-monitor-master`.
	2. Install the debian package using
		```
		sudo dpkg -i ../*.deb
		sudo apt install -f
		```
### Other Linux-based systems
1. Install the [dependencies](#other-linux-based-distro).
2. From instructions for [Debian/Ubuntu based systems](#debianubuntu-based-systems), follow **Option 1**.

### For Developers
Now you can automatically test **Battery Monitor** from Terminal:

```
python3 run.py --test
```
Or, if you've already installed:

```
battery-monitor --test
```

**I have no knowledge on how to use `meson` or `npm` for testing. If you can offer any help regarding this, please start a discussion [here](https://github.com/hsbasu/battery-monitor/discussions) or create a [PR](https://github.com/hsbasu/battery-monitor/compare). It will be more than welcome.**

## User Manual

### Auto Start
Every time Battery Monitor starts automatically after PC boots up. It pops up notifications and you see its **Icon** in the system tray. To reveal the other beauties, you can click on the icon. Currently, there are three menus: **Settings**, **About** and **Quit**.

You can also start battery monitor from the menu entries. Please, search for Battery Monitor launcher in the menu entries and simply click on it. In case, if Battery Monitor doesn't start automatically, please open an [issue](#issue-tracking-and-contributing). We would like to debug the issue and help you.

## Issue Tracking and Contributing
If you are interested to contribute and enrich the code, you are most welcome. You can do it by:
1. If you find a bug, to open a new issue with details: [Click Here](https://github.com/hsbasu/battery-monitor/issues)

2. If you know how to fix a bug or want to add new feature/documentation to the existing package, please create a [Pull Request](https://github.com/hsbasu/battery-monitor/compare).

**NB:** Using the issue template or PR template is **not** mandatory.

## Contributors

### [Himadri Sekhar Basu](https://hsbasu.github.io)
Current Maintainer.

### [Maksudur Rahman Maateen](https://github.com/maateen)
He is the original creator of now archived [Battery Monitor](https://github.com/maateen/battery-monitor). We are highly grateful to him for offering this useful app and providing the base for the current [Battery Monitor](https://github.com/hsbasu/battery-monitor). Please take a minute to thank him.

### [Safwan Rahman](https://github.com/safwanrahman)

He has reformatted the code in a new style. The style represents the code easier to understand. Also, he has optimized the code in a way that **Battery Monitor** consumes a little resource of your PC. Please take a minute to thank him.

### [Abdelhak Bougouffa](https://abougouffa.github.io/)

He has fixed some bugs and optimized **Battery Monitor** in a way so that it consumes lower CPU and RAM than before. Please take a minute to thank him.

### [Yochanan Marqos](https://github.com/yochananmarqos)

He is our official package maintainer in AUR. He has put Arch users' life at ease. Please take a minute to thank him.

### [Benjamin Staffin](https://github.com/benley)

He has improved the build process and added modern Python setuptools packaging. Please take a minute to thank him.

## Donations
If you like this app and would like to buy me a :coffee:, you can do so via:

<a href="https://liberapay.com/hsbasu/donate"><img alt="Donate using Liberapay" src="https://liberapay.com/assets/widgets/donate.svg"></a>

<a href="https://paypal.me/hsbasu"><img alt="Donate using PayPal" src="https://www.paypalobjects.com/webstatic/i/logo/rebrand/ppcom.svg"></a>