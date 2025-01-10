<img align="right" src="https://github.com/kadarej/woa-marble/blob/main/marble.png" width="350" alt="Windows 11 running on marble">

# Running Windows on the POCO F5/Redmi Note 12 Turbo

## Troubleshooting Issues
> Below you will find a list of common problems and their solutions

## USB does not work
Enable USB host mode using the optional [post install guide](materials.md#toggling-usb-host-mode).

##### Finished!

## Error: 3 The system cannot find the path specified.
This error usually means that you are trying to install Windows on a disk that already has Windows installed. To solve this issue, format the disk in Windows Explorer and try again.

##### Finished!

## 0xc000021a BSOD
This usually means that winlogon.exe has failed, and you may need to reapply the Windows image.

##### Finished!

## The computer restarted unexpectedly or encountered an unexpected error
If you stumble upon this error, you will need to [reinstall Windows](reinstall.md).

##### Finished!

## INACCESSIBLE_BOOT_DEVICE BSOD
This Blue Screen of Death likely means some broken driver installation. To fix this, [reinstall Windows](reinstall.md).

##### Finished!
