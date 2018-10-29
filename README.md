# iBasso DX120 firmware modified by Lurker

**DISCLAIMER:** No changes were made to the basic player functionality and behavior! Expect the same bugs and misbehavior found in the base stock firmware! **No warranty at all: use the modified firmware at your own risk and responsibility!**

**NOTE:** to tell which version is running, go to _Settings_->_Advanced_->_System Info_ and check the _Model number_. The modification version number (L0, L1 etc) is right after the actual model number (DX120).

# Recommended firmware update procedure
Often a firmware update requires subsequent factory reset for problemless use. The following procedure ensures factory reset without additional efforts:
1. Unzip downloaded archive and put resulting `update.img` file into the root folder of a microSD card.
2. Turn the device off.
3. Insert the miscroSD card to any slot, but be sure the other slot is empty!
4. Press and hold Volume+ button, then turn the power on.
5. Wait for recovery menu to appear. Release Volume+ button.
6. Using volume buttons, select *Apply update from SDcard*
7. Push Power button to select.
8. Wait for firmware updating, data and cahe partitions formatting (which is the factory reset) and reboot to the new version.

# Detailed description of the changes

## Introduction for those who seeks the sound quality
All firmware versions for iBasso DX120, stock or with my modifications, are bit perfect. It means, with EQ turned off, the *sound data is not affected by the software, and is transferred to the DAC exactly as it is*. Any difference in sound signatures between versions are resulted from different conditions under which the hardware is running.

In DAPs, with limited space and one battery as the power source for both digital and analog circuits, the sound signature also depends on CPU load. So, any changes in the firmware code, even unrelated directly to the sound path, may affect the sound signature.

## 1. Fonts replaced

iBasso uses `PingFang SC Regular` for Latin-based and Chinese characters, and `Nimbus Sans Global Bold` for the rest (Cyrillic, Japanese, Korean, Thai etc). It also uses pre-calculated character width tables, which (confirmed by calculations!) do not correspond to any, or any combination, of those fonts. Regardless of the reason iBasso went this way, the resulting texts look awful for me.

The two fonts used by iBasso are replaced with one, which is `Roboto Condensed`, with the missing characters merged from `Arial Unicode MS`. Character width tables were calculated from the actual font metrics.

For those who prefer original fonts, I make special fimware builds.

## 2. CPU is always working at the highest performance

By default, Android uses `interactive` CPU performance governor, meaning, CPU frequency depends on a load and may be changed. Changes in the CPU working frequency during audio playback affect the stability of the power source and temperature, probably, also the stability of the sound stream from CPU to DAC. So, stable CPU speed also means stable power and temperature of other components: DAC, clock generator, op-amps. This firmware forces `performance` governor, i.e. always highest supported frequency.

Keep CPU running at the highest speed (1.2GHz for DX120) does not mean to drain more power: Linux/Android kernel is smart enough to halt a CPU core if it is not actually used. Also, CPU is not the main power consumer: display, flash, RAM, DAC and analog part (including headphone amplifier) in total consume much more.

## 3. Ultimate cleanup

iBasso uses stripped down Android, leaving a lot of processes and services that have no use. In my fimrware builds, `MangoPlayer` is the only running process, apart from the `kernel` and `init`, which are required, obviously!

DX120 is built using the same platform as DX80. Please refer to [DX80 very detailed firmware description](https://github.com/Lurker00/DX80-firmware/blob/master/release/README.md#9-ultimate-cleanup) if you are curious what exactly was removed.

## 4. Image size reduced

I've removed the firmware parts that were not changed since the very first factory build. It makes download and flashing faster, but these images are not suitable for flashing a device with fully erased memory. If you, by a chance, need to flash an empty device, please first use any stock firmware, then upgrade to such a build.
