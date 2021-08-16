# Counterfeit RTC

## Summary

For some 300 series motherboards, the `RTC` device is disabled by default and it is not possible to enable the traditional RTC device by controlling the return value of `_STA` through the `STAS` variable shared with `AWAC`, resulting in ***`SSDT-AWAC` *** Cannot take effect, so in order to force the `RTC` device to be enabled, we need to fake a `RTC0`.

## Instructions

> Case

```Swift
Device (RTC)
{
  Name (_HID, EisaId ("PNP0B00"))
  Name (_CRS, ResourceTemplate ()
  {
      IO (Decode16,
          0x0070,
          0x0070,
          0x01,
          0x08,
         )
      IRQNoFlags ()
          {8}
  })
  Method (_STA, 0, NotSerialized)
  {
    Return (0);
  }
}
```

> The above is the case where the `RTC` device is disabled. The counterfeiting method is as follows:

```swift
DefinitionBlock ("", "SSDT", 2, "ACDT", "RTC0", 0)
{
    External (_SB_.PCI0.LPCB, DeviceObj)

    Scope (_SB.PCI0.LPCB)
    {
        Device (RTC0)
        {
            Name (_HID, EisaId ("PNP0B00"))
            Name (_CRS, ResourceTemplate ()
            {
                IO (Decode16,
                    0x0070,
                    0x0070,
                    0x01,
                    0x08,
                    )
                IRQNoFlags ()
                    {8}
            })
            Method (_STA, 0, NotSerialized)
            {
                If (_OSI ("Darwin"))
                {
                    Return (0x0F)
                }
                Else
                {
                    Return (0);
                }
            }
        }
    }
}
```

## Notice

-This component is only valid for 300 series motherboards.
-This component is only used when ***`SSDT-AWAC`*** is not used and the return value of the `_STA` method of the `RTC` device in the original `ACPI` is `0`.
-The device path of the sample patch is `LPCB`, please modify it according to the actual situation.