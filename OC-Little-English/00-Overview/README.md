# Overview

## ACPI name change and patch

-Do not use or use less renames and patches as much as possible. For example: `HDAS rename HDEF`, `EC0 rename EC`, `SSDT-OC-XOSI` and so on. Especially for the underlined `MethodObj` (such as _STA, _OSI, etc.) to be **used with caution**. In general:
  -No operating system patch required. For components that cannot work normally due to system limitations, patches are customized according to the specific conditions of ACPI. **Use with caution** "Operating System Patches" that have special requirements for the operating system.
  
  -Most machines no longer need the brightness shortcut key rename and patch. See "PS2 Keyboard Mapping and Brightness Shortcuts", "Special Patches for Branded Machines".
  -For now, most machines need "0D6D Patch" to solve the `second wakeup` problem.
  -For the battery part, see "Notebook Battery Drive".
  -Most Thinkpad machines need "PTSWAK Comprehensive Extension Patch" to solve the problem that the breathing light does not recover after waking up.
  -For machines with a sleep button [little moon], if the system crashes after pressing this button, please refer to "PNP0C0E Sleep Correction Method".
-The solution of some problems requires enabling or disabling certain devices. The methods to enable or disable the device are:
  -"Binary renaming and preset variables"-Binary renaming is very effective for single systems. For multiple systems, the impact of the name change on other systems should be evaluated. **Use with caution**. The preset variables may affect other components or other systems. **Use with caution**.
  -"Counterfeit Equipment"-This method is very reliable. **Recommended Use** .

## Important patch

-***SSDT-RTC0***-located in "Counterfeit Devices"

  Some machines cause system crash during startup due to RTC [PNP0B00] being disabled. Use ***SSDT-RTC0*** to solve this problem.

-***SSDT-EC***-located in "Counterfeit EC"

  For **10.15+** system [notebook], if the EC controller name is not `EC`, you need to add ***SSDT-EC***, otherwise the system will crash during startup.