<img align="right" src="https://github.com/kadarej/woa-marble/blob/main/marble.png" width="350" alt="Windows 11 running on marble">

# Running Windows on the POCO F5/Redmi Note 12 Turbo

## Partitioning your device

### Prerequisites
- Unlocked bootloader

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Modded OFOX](https://github.com/kadarej/woa-marble/releases/download/Files/modded-ofox-marble.img)

### Notes
> [!WARNING]  
> 
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/WinOnMarble).
> 
> Do not run all commands at once, execute them in order!

### Opening CMD as an admin
> Download **platform-tools** and extract the folder somewhere, then open CMD as an **administrator**.
>
> It is recommended to keep this window open and use it throughout the entire guide.
> 
> Replace `path\to\platform-tools` with the actual path to the platform-tools folder, for example **C:\platform-tools**.
```cmd
cd path\to\platform-tools
```

#### Flash the modded OFOX recovery
> Replace `path\to\modded-ofox-polaris.img` with the actual path of the image
```cmd
fastboot flash recovery path\to\modded-ofox-polaris.img reboot recovery
```

### Backing up important files
> This will back up **devinfo**, **persist**, **fsc** **fsg**, **modemst1** and **modemst2** to the current path your CMD is opened in (for example **C:\platform-tools**). Confirm these files are actually there before proceeding.
>
> Keep these backups in a safe place. If your device's software ever gets destroyed, you might need these backups or your phone could lose cellular capabilities.
>
> If you've got anything else you want to back up, do this now. Your Android data will be erased in the next steps.
```cmd
cmd /c "for %i in (devinfo,persist,fsg,fsc,modemst1,modemst2) do (adb shell dd if=/dev/block/by-name/%i of=/tmp/%i.bin & adb pull /tmp/%i.bin)"
```

#### Backing up your boot image
> This will back up your boot image in the current directory
```cmd
adb pull /dev/block/by-name/boot$(getprop ro.boot.slot_suffix) boot.img
```

### Partitioning your device
> There are two methods to partition your device. Please select the method you would like to use below. 

#### Method 1: Manual partitioning 

<details>
  <summary><strong>Click here for method 1</strong></summary> 

#### Unmount data
> Ignore any possible errors and continue
```cmd
adb shell /
umount /data /
umount /sdcard /
umount /metadata /
lptools unmap userdata /
``` 

#### Preparing for partitioning
```cmd
adb shell parted /dev/block/sda
``` 

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list
```cmd
print
``` 

#### Removing userdata
> Replace **$** with the number of the **userdata** partition, which should be **33**
```cmd
rm $
``` 

#### Recreating userdata
> Replace **12.7GB** with the former start value of **userdata** which we just deleted
>
> Replace **212.7GB** with the end value you want **userdata** to have. In this example your available usable space in Android will be 212.7GB-12.7GB = **200GB**
```cmd
mkpart userdata ext4 12.7GB 212.7GB
``` 

#### Creating ESP partition
> Replace **212.7GB** with the end value of **userdata**
>
> Replace **213GB** with the value you used before, adding **0.3GB** to it
```cmd
mkpart esp fat32 212.7GB 213GB
``` 

#### Creating Windows partition
> Replace **213GB** with the end value of **esp**
```cmd
mkpart win ntfs 32.3GB -0MB
``` 

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be **22**
```cmd
set $ esp on
``` 

#### Exit parted
```cmd
quit
``` 

### Formatting data
- Format all data in recovery, or Android will not boot.
- ( Go to Wipe > Format data > type yes ) 

#### Check if Android still starts
- Just restart the phone, and see if Android still works 

### Formatting Windows and ESP drives
> Reboot into the modded recovery, then run the below two commands
```cmd
adb shell mkfs.ntfs -f /dev/block/by-name/win -L WINMARBLE
``` 

```cmd
adb shell mkfs.fat -F32 -s1 /dev/block/by-name/esp -n ESPMARBLE
``` 

</details>

#### Method 2: Automatic partitioning 

<details>
  <summary><strong>Click here for method 2</strong></summary> 

### Run the partitioning script
> Replace **$** with the amount of storage you want Windows to have (do not add GB, just write the number)
> 
> If it asks you to run it once again, do so
```cmd
adb shell partition $
``` 

### Check if Android still starts
- Just restart the phone, and see if Android still works 

</details>

## [Next step: Rooting your phone](/guide/2-root.md)
