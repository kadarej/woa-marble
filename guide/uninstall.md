<img align="right" src="https://github.com/kadarej/woa-marble/blob/main/marble.png" width="350" alt="Windows 11 running on marble">

# Running Windows on the POCO F5/Redmi Note 12 Turbo

## Uninstallation

### Why is this needed?
If you want to uninstall windows this is used instead of deleting partitions manually to avoid human error + writing a whole dedicated guide to just uninstalling.

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [gpt_both0.bin](https://github.com/kadarej/woa-marble/releases/download/Files/gpt_both0.bin)

### Uninstall instructions
### Method 1
#### Boot into fastboot mode
> Hold the volume down + power button while the phone is turned off, or run the following command while it is booted
```cmd
adb reboot bootloader
```

#### Restore GPT
> Replace ```path\to\gpt_both0.bin``` with the path to the gpt_both0.bin file.

```cmd
fastboot flash partition:0 path\to\gpt_both0.bin
```

#### Erase userdata
> To avoid a bootloop and restore FS size
```cmd
fastboot -w
```
> [!Note]
> If erasing userdata fails, reboot to recovery and wipe all data there instead

## Finished!

### Method 2
#### Boot into twrp
> Hold the volume up + power button while the phone is turned off, or run the following command while it is booted
```cmd
adb reboot recovery
```
#### Restore GPT
```cmd
adb shell restore
```

## Finished
