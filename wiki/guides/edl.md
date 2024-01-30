---
title: Fastboot and EDL
parent: Customization
layout: default
---
{:.no_toc}

Table of Contents
{: .text-delta }
- TOC
{:toc}

# Fastboot

---
# EDL

**Qualcomm Emergency Download mode**, commonly known as EDL mode, is a special engineering interface implemented on devices with Qualcomm chipsets. Its purpose is to perform special operations on the phone that are intended for device manufacturer only, such as unlocking the bootloader, read and flash firmwares on the phone's filesystem or recover it from being a dead paperweight. Unlike bootloader or Fastboot mode, system files needed by the EDL mode resides on a separate 'primary bootloader' that cannot be affected by software modifications. 

Aleph Security has a deep-dive blog post into exploiting the nature of EDL mode on Qualcomm-chipset devices that you can read [here](https://alephsecurity.com/2018/01/22/qualcomm-edl-1).

Booting into this mode, the phone's screen will turn almost black as if it has been turned off, but in fact it still receives commands over Qualcomm's proprietary protocol called Sahara (Firehose on newer devices). With a [suitable digitally-signed programmer in MBN/ELF file format](https://edl.bananahackers.net) and some instruction-bundled tools, the most popular one being QFIL (Qualcomm Flash Image Loader), one can send commands from a computer to the phone over USB.

For the sake of cross-platform usage (and our obsession of open-source tools), instead of QFIL which is proprietary and only supports Windows, we'll be using open-sourced Python scripts from GitHub, such as [bkerler's](https://github.com/bkerler/edl) and [andybalholm's](https://github.com/andybalholm/edl) that are great as alternatives.

## Booting into EDL mode
### Using button combos
Depending on the form factor and the motherboard's design, each device model has different button combos that can be hold down while inserting the USB cable to trigger the circuits into switching to EDL mode.

**While plugging in the USB cable or holding the Power button:**

- Nokia 8110 4G, Nokia 800 Tough: hold both D-Pad Up and Down;
- CAT B35, Nokia 8000 4G, Nokia 6300 4G: hold both * and #;
- Nokia 2720 Flip: hold both the side volume keys. Be careful not to accidentally press the SOS button.
- Alcatel Cingular Flip: hold both volume keys until you see the booting logo blinks, then hold only one of them.

If you manage to get it, the booting logo will flash momentarily, then the screen turns black as if you've turned off the phone. Else, the normal boot sequence will be triggered instead, and you'll have to start over.

### Using Android Debug Bridge `adb`
While having the phone on and connected to the computer via an USB cable, turn on debugging mode on the phone and set up ADB on your computer (see [Sideloading and debugging/ADB and WebIDE]({% link development/webide.md %})), then in the command-line window, type in `adb reboot edl`. This will send a signal to your phone telling to reboot to EDL mode.

Don't use this if you're unbricking your phone.
 
### Using an EDL cable
An EDL cable is an USB cable that specializes in transmitting signals for EDL mode between your phone and computer.

You can make an EDL cable for yourself by stripping the insulation of a spare USB cable and wiring part of D+ and Ground wires in a way that sends the signal to tell the phone to switch to EDL mode. [Here's a specific guide on how to do just that.]({% link error.md %})

Alternatively, you can find lots of pre-made EDL cables online for as cheap as $2 in Philippines (citing Cyan). Pre-made EDL cables has a button attached: while holding down the button, insert the cable to the device, wait for 5 seconds and then you can let it go.

### Disassembling the phone

> This method is RISKY and mainly used by professionals, as it requires you to disassemble your phone, find and short the pins that trigger the primary bootloader, which in turn boot your phone in EDL mode. If you don't know what you're doing, you can damage your phone in the process altogether. **Proceed with caution.**
> 
> A dedicated guide for this method can be found [here]({% link error.md %}).
{:.is-warning}

## Exiting EDL mode
This is just as critical to know, because if the EDL utility happened to not work properly (wrong programmer?), you wouldn't be able to enter any reset command from EDL to exit this mode.

### Removing the battery
On devices with removable battery, taking the battery off will shut the phone down and (abruptly) also exit EDL mode in the process.

### Using another button combo
On most devices, there's also a button combo hardcoded for force rebooting the device at any time. This is normally useful when the system hangs up, but also comes in handy if you want to exit EDL mode. 

i.e. To exit EDL mode on the Nokia 800 Tough — which has non-removable battery — hold both the Power/End call and D-Pad Down keys (just pressing Power/End call won't work).

![luxferre.png](/edl/luxferre.png)

### Wait
If you can't either get the combo button to work or open the phone... Welp, the last option is to wait for eternity for the battery to die.

## Setting up environment for EDL tools
### Know the diffs
- **Qualcomm Flash Image Loader (QFIL)** is a Windows-only graphical tool and is more commonly used since it provides a more user-friendly interface to work with EDL mode. To use QFIL, in addition to the programmer, you need to have `rawprogram0.xml`, `patch0.xml` and a QFIL-compatible ROM.
- **[bkerler's edl-3.1](https://github.com/bkerler/edl/releases/tag/3.1)**, on the other hand, is a cross-platform command-line tool, but doesn't need the XML files. Compatible with newer GPT partition tables found in Nokia 8000 4G, Nokia 6300 4G and Alcatel MyFlip (A405DL).
- **[andybalholm's edl](https://github.com/andybalholm/edl)** is also a cross-platform command-line tool, but is more compatible with older GPT partition tables found in Nokia 8110 4G, Nokia 2720 Flip, Nokia 800 Tough, Maxcom MK241 and CAT B35.

Once you've decided which EDL package you want to use, find and download the correct [firehose programmer for your device](https://edl.bananahackers.net). Extract the EDL package in a folder and put the MBN file at the root of that folder.

> Now, if you wish to use QFIL, please skip to its dedicated section.
{:.is-info}

### Linux
{:.no_toc}

1. Open Terminal and install Python and `pip3` from your operating system's package manager i.e.

```
$ sudo apt-get install python pip3 adb
```

2. Then, type this to install the dependencies for EDL tools:
{:style="counter-reset:none"}

```
$ sudo -H pip3 install pyusb pyserial capstone keystone-engine docopt
```

3. Switch your phone to EDL mode and connect it to your computer.
{:style="counter-reset:none"}

Additionally, if you have issue with device access:

- Open `/etc/modprobe.d/blacklist.conf` in a text editor and append `blacklist qcserial`.
- Copy both `51-edl.rules` and `50-android.rules` in the root of extracted EDL tools folder to `/etc/udev/rules.d`.

### macOS
{:.no_toc}

We'll be using Homebrew to quickly set up Python, `pip3` and dependencies for the EDL tools. You can also install Python directly from [its homepage](https://python.org) and set up that way if you prefer.

1. Follow the instructions to install Homebrew on [its homepage](https://brew.sh). Basically just open Terminal and copy the long streak of code shown on the page, and type your password when prompted.
2. While you're in Terminal, type this into the command-line:

```
brew install python android-platform-tools libusb &&
pip3 install pyusb pyserial capstone keystone-engine docopt
```

3. Switch your phone to EDL mode and connect it to your computer.
{:style="counter-reset:none"}

### Windows
{:.no_toc}

1. Download the [Python installer](https://www.python.org/downloads) from its homepage and proceed with installation. Remember to tick the box next to "Add Python 3.x to PATH". This would make Python able to be called everywhere in the command-line instead of specifically pointing to its folder, which the next part of the guide won't cover on.

![python.png](/edl/python.png)

2. Open Command Prompt with administrator privileges and run this command:
{:style="counter-reset:none"}

```
pip3 install pyusb pyserial capstone keystone-engine docopt
```

![pythoooon.png](/edl/pythoooon.png)

3. Open the extracted EDL tools folder, go to the Drivers > Windows folder and run `Qualcomm_Diag_QD_Loader_2016_driver.exe` with administrator rights. Proceed with installation and leave everything as default, restart the computer if it prompts you to do so.
{:style="counter-reset:none"}

![whatever.png](/edl/whatever.png)

4. Switch your phone to EDL mode and connect it to your computer.
{:style="counter-reset:none"}

5. Download and run [Zadig 2.7](https://github.com/pbatard/libwdi/releases/tag/v1.4.1) (use this version and NOT the one provided by the EDL package). Select Options > List All Devices.
{:style="counter-reset:none"}

![listall.png](/edl/listall.png)

6. In the front dropdown menu, select `QHSUSB__BULK` (your device in EDL mode). 
{:style="counter-reset:none"}

![qhsusb.png](/edl/qhsusb.png)

7. In the target driver box (which the green arrow is pointing to), click on the up/down arrows until you see `libusb-win32` and click on Replace Driver.
{:style="counter-reset:none"}

![arg.png](/edl/arg.png)

8. If you're installing the driver for the first time, an "USB Device Not Recognised" pop-up may appear. Exit EDL mode by removing and re-inserting the battery, then turn on the phone in EDL mode again.
{:style="counter-reset:none"}

## bkerler's edl-3.1
Open Terminal/Command Prompt and use `cd` to redirect to the EDL tools folder you've just extracted. The tool assumes you've moved the image files/folders needed into its root folder.

> Replace `[loader.mbn]` with the firehose programmer/MBN file you have, exclude the brackets i.e. `--loader=8110.mbn`.
{.is-info}

1. **Get the GPT partition table layout:**

```
python edl.py printgpt --loader=[loader.mbn]
```

2. **Dump the content of partition(s):**
{:style="counter-reset:none"}

```
python edl.py r [partition1,partition2...] [file1,file2...] --loader=[loader.mbn]
```
i.e. `python edl.py r boot boot.img --loader=8k.mbn`
`python edl.py r boot,system boot.img,system.img --loader=2720.mbn`

You can dump the content of multiple partitions with:

```
python edl.py rl [folder_dir] --skip=[partition_name] --genxml --loader=[loader.mbn]
```
i.e. `python edl.py rl dumps --skip=userdata,cache --genxml` will dump the content of all partitions in the phone's filesystem into `dumps` directory, EXCEPT `userdata` and `cache`, and also generate a `rawprogram0.xml` in the process.

3. **Flash an image file onto a partition:**
{:style="counter-reset:none"}

```
python edl.py w [partition_name] [filename] --loader=[loader.mbn]
```
i.e. `python edl.py w boot boot.img --loader=8k.mbn`

You can flash multiple images in a directory to respective partitions:

```
python edl.py wl [folder_dir] --loader=[loader.mbn]
```

4. **Erase the content of a partition:**
{:style="counter-reset:none"}

```
python edl.py e [partition_name] --loader=[loader.mbn]
```

5. **Reboot the phone:**
{:style="counter-reset:none"}

```
python edl.py reset
```
For the full list of commands, including dumping/writing raw BIN image files and sectors, you can type `python edl.py -h` or consult the tool's [GitHub repository](https://github.com/bkerler/edl).

## andybalholm's edl
Open Terminal/Command Prompt and use `cd` to redirect to the EDL tools folder you've just extracted. The tool assumes you've moved the image files/folders needed into its root folder.

> Replace `[loader.mbn]` with the firehose programmer/MBN file you have, exclude the brackets i.e. `-loader 8110.mbn`.
{.is-info}

1. **Get the GPT partition table layout:**

```
python edl.py -loader [loader.mbn] -printgpt
```

2. **Dump the content of partition(s):**
{:style="counter-reset:none"}

```
python edl.py -loader [loader.mbn] r [partition_name] [filename]
```
i.e. `python edl.py -loader 2720.mbn -r boot boot.img`

3. **Flash an image file onto a partition:**
{:style="counter-reset:none"}

```
python edl.py -loader [loader.mbn] w [partition_name] [filename]
```
i.e. `python edl.py -loader 800t.mbn w boot boot.img`

4. **Erase the content of a partition:**
{:style="counter-reset:none"}

```
python edl.py -loader [loader.mbn] e [partition_name]
```

5. **Reboot the phone:**
{:style="counter-reset:none"}

```
python edl.py reset
```

## QFIL

> Although this program is more friendly than the other twos, unfortunately I haven't got this to work. You can find lots of tutorials on QFIL online! If you manage to get the program to work, please contribute to this section — I'd really appreciate it!
{:.is-info}