# CRAP

Note: This project was originally forked from [reynhout/chrx](https://github.com/reynhout/chrx).
The project has been completely rewritten since, and is now only a partitioning tool.
It does not include any feature to install an alternate operating system, you must do that yourself.

This tool works on all Chromebook models. See [documentation](https://docs.chrultrabook.com/docs/firmware/supported-devices.html).

## Features

#### Resize stateful partition

Resize the user-data partition on the disk to make room for an alternate OS.
This script supports non-destructive resizing of the filesystem, so you won't
have to worry about your data being wiped!

#### Reorder 1-sector partitions

Fix a bug that causes libparted to error and be unable to detect existing partitions.
If you're installing an operating system that uses an affected version of libparted, you will need
to do this or the installer will fail to recognize existing partitions, which effectively wipes
the disk when you install it.  
See [this bug](https://lists.gnu.org/archive/html/bug-parted/2022-04/msg00004.html) for more info.

#### Re-create stateful filesystem

Reset the ChromeOS user data partition to a factory state.

## Usage

Running this script does not require you to have valid RW_LEGACY firmware installed,
but this is currently the recommended method for dual booting another operating system alongside ChromeOS on x86_64-based hardware.
See [MrChromebox's Firmware Utility Script](https://mrchromebox.tech/#fwscript) for installing RW_LEGACY firmware.

### Running the script

1. Ensure you're in developer mode and connected to WiFi.
2. Open VT2 using `[ Ctrl ] [ Alt ] [ → ]` (F2), login as `root` (not `chronos`)
	- Note: the script *cannot* be run with crosh on any version of ChromeOS.
	- Note 2: you can also run the script while booted into your alternate OS!
3. Run the script!
	- Run `bash <(curl https://raw.githubusercontent.com/chrultrabook/crap/master/crap)`
4. The script will walk you through the steps to make room for an alternate OS.

## Screenshots

CRAP - main menu

![Screenshot - CRAP - main menu](/screenshots/screenshot01.png)

CRAP - resizing stateful partition

![Screenshot - CRAP - resizing stateful partition](/screenshots/screenshot02.png)

## Notes

* We do NOT EVER use the KERN-C or ROOT-C partitions NO

## Acknowledgements

- [MrChromebox/scripts](https://github.com/MrChromebox/scripts), for reference
- [chromeos-common](https://chromium.googlesource.com/chromiumos/platform2/+/main/chromeos-common-script/share/chromeos-common.sh), for some adapted code (namely get_largest_nvme_namespace)
- [reynhout/chrx](https://github.com/reynhout/chrx)'s setup-storage script, for reference
- bendavis78's [resize-stateful-partition](https://gist.github.com/bendavis78/5929b46efd26232d7e9e), for reference
- honorable mention: [ethanmad/chromeos-resize](https://github.com/ethanmad/chromeos-resize)
