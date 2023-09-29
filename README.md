# FuntooWSL
Funtoo Linux on WSL2
inspired by [FuntooWSL](https://github.com/rescenic/FuntooWSL)
based on [wsldl](https://github.com/yuk7/wsldl).

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
![License](https://img.shields.io/github/license/Vinfall/ClearWSL.svg?style=flat-square)

**Notice: This is UNOFFICIAL and not affiliated with Funtoo Linux.**

## Requirements
* Windows 10 Fall Creators Update x64 or later.
* Windows Subsystem for Linux feature is enabled.

## Install

1. Check [How to build](#how-to-build) and do it yourself. ~~Download installer zip from [release](https://github.com/Vinfall/FuntooWSL/releases/latest) or [weekly action build](https://github.com/Vinfall/FuntooWSL/releases/tag/action-build) (recommended)~~
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

### exe Usage
```dos
Usage :
    <no args>
      - Open a new shell with your default settings.
    run <command line>
      - Run the given command line in that distro. Inherit current directory.
    config [setting [value]]
      - `--default-user <user>`: Set the default user for this distro to <user>
      - `--default-uid <uid>`: Set the default user uid for this distro to <uid>
      - `--append-path <on|off>`: Switch of Append Windows PATH to $PATH
      - `--mount-drive <on|off>`: Switch of Mount drives
    get [setting]
      - `--default-uid`: Get the default user uid in this distro
      - `--append-path`: Get on/off status of Append Windows PATH to $PATH
      - `--mount-drive`: Get on/off status of Mount drives
      - `--lxuid`: Get LxUID key for this distro
    backup
      - Output backup.tar.gz to the current directory using tar command.
      
    clean
      - Uninstall the distro.
    help
      - Print this usage message.
```

### How to uninstall instance
```dos
>Funtoo.exe clean
```

## How to build

```sh
# Build
git clone https://github.com/Vinfall/FuntooWSL
cd FuntooWSL
sudo make

# Clean
#sudo make clean
```

The output `FuntooWSL.zip` would be as large as 1GB, this is normal so don't panic.
If you want to use newer stage3 rootfs or [subarches](https://www.funtoo.org/Subarches) optimized for your CPU, replace `BASE_URL` in Makefile.

By the way, I use Gentoo icon instead of Funtoo to avoid compiling wsldl, as [the one provided by rescenic](https://github.com/rescenic/FuntooWSL/raw/master/res/Funtoo/icon.ico) is a meme.

## License

MIT

Copyright (c) 2020-2021 Rescenic

Copyright (c) 2023 Vinfall
