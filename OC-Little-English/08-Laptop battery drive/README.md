# Laptop battery drive

-Generally, the driving method of laptop battery is: drive (***SMCBatteryManager.kext*** or ***ACPIBatteryManager.kext*** + SSDT patch. The function of SSDT patch is to split multi-byte data into multiple Single-byte data to meet the driver's read and write requirements. The actual process of making SSDT patches is more complicated, cumbersome, and error-prone. The random device is different and it is difficult to form a universal patch.

-The development of ***ECEnabler.kext*** successfully solved the above problems. It replaces the role of the patch, it works well on most laptops, and the SSDT patch is no longer needed.

-For the content of ***ECEnabler.kext***, please refer to https://github.com/1Revenger1/ECEnabler/releases

-**Note:** At this stage, ***ECEnabler.kext*** may not be applicable to all notebooks. The battery patch of some machines still requires the SSDT patch method. For these contents, please refer to the "Battery Patch" of "Reserved Parts".