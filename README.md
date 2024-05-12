# FuntooWSL

Funtoo Linux on WSL2
inspired by [FuntooWSL](https://github.com/rescenic/FuntooWSL)
based on [wsldl](https://github.com/yuk7/wsldl).

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
![License](https://img.shields.io/github/license/Vinfall/FuntooWSL.svg?style=flat-square)

**Notice: This is UNOFFICIAL and not affiliated with Funtoo Linux.**

## Requirements

* Windows 10 1803 April 2018 Update x64 or later.
* Windows Subsystem for Linux feature is enabled.
* Latest WSL recommended.

## Install

1. Check [How to build](#how-to-build) and do it yourself, or download installer zip from [release](https://github.com/Vinfall/FuntooWSL/releases).
2. Extract all files in zip file to same directory (e.g. `C:\WSL\Funtoo`)
3. Run `Funtoo.exe` to Extract rootfs and Register to WSL

Exe filename is using to the instance name to register.
If you rename it, you can register with a different name and have multiple installs.

## Init

```sh
# Setup repo
epro show
ego sync
# Update Funtoo Linux to latest
emerge -auDN @world
# Remove obsolete packages after world updates
emerge --ask --depclean
```

The commands above does not setup portage and compiler for you as they are personal and bound to change according to your system.
You may refer to [Funtoo Linux Installation Guide](https://www.funtoo.org/InstallPrintable), [Emerge](https://www.funtoo.org/Emerge) and [rescenic/FuntooWSL#first-setup](https://github.com/rescenic/FuntooWSL#first-setup) for further instruction.

## How-to-Use (for Installed Instance)

### Usage

```powershell
Usage :
    <no args>
      - Open a new shell with your default settings.

    run <command line>
      - Run the given command line in that distro. Inherit current directory.

    runp <command line (includes windows path)>
      - Run the path translated command line in that distro.

    config [setting [value]]
      - `--default-user <user>`: Set the default user for this distro to <user>
      - `--default-uid <uid>`: Set the default user uid for this distro to <uid>
      - `--append-path <on|off>`: Switch of Append Windows PATH to $PATH
      - `--mount-drive <on|off>`: Switch of Mount drives
      - `--default-term <default|wt|flute>`: Set default terminal window

    get [setting]
      - `--default-uid`: Get the default user uid in this distro
      - `--append-path`: Get on/off status of Append Windows PATH to $PATH
      - `--mount-drive`: Get on/off status of Mount drives
      - `--wsl-version`: Get WSL Version 1/2 for this distro
      - `--default-term`: Get Default Terminal for this distro launcher
      - `--lxguid`: Get WSL GUID key for this distro

    backup [contents]
      - `--tgz`: Output backup.tar.gz to the current directory using tar command
      - `--reg`: Output settings registry file to the current directory

    clean
      - Uninstall the distro.

    help
      - Print this usage message.
```

### Uninstall

```powershell
.\Funtoo.exe clean
```

## How to build

FuntooWSL can be built on GNU/Linux or WSL.

`curl`, `bsdtar`, `jq` and `unzip` is required for build.

```sh
# Build FuntooWSL
sudo apt install -y curl libarchive-tools jq unzip
git clone https://github.com/Vinfall/FuntooWSL
cd FuntooWSL
# Use of `sudo` recommended to avoid weird file permission in rootfs
sudo make

# Backup build
sha512sum Funtoo.zip > Funtoo.zip.sha512
mv Funtoo.zip* some/where/secure/

# Clean-up using `sudo` as some files are owned by root
sudo make clean
```

The output `Funtoo.zip` would be as large as 1GB, this is **normal** so don't panic.
If you want to use newer stage3 rootfs or [subarches](https://www.funtoo.org/Subarches) optimized for your CPU, replace `BASE_URL` in Makefile.

By the way, I use Gentoo icon instead of Funtoo to avoid compiling wsldl, as [the one provided by rescenic](https://github.com/rescenic/FuntooWSL/raw/master/res/Funtoo/icon.ico) is a meme.

## License

MIT

Copyright (c) 2020-2021 Rescenic

Copyright (c) 2023-2024 Vinfall
