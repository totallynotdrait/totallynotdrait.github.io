# Boot Config

Boot Config is a data structure defined in both the bootloader and kernel of Atlas.
It contains different values that are defined by the bootloader and passed to the kernel entry point (`AAiSystemStartup`).

Specifically it contains:
 - A struct containing information about the framebuffer
 - A struct to the default PSF1 font 
 - EFI memory map and descriptor size
 - The boot type


## Boot Type

The Boot Type is a value defined in the Boot Config struct that tells the kernel how it needs to boot.

The Boot Type can be changed by the boot menu or from a user input while bootloader boot splash.

Boot Types:
 - `0x0` Normal boot:                       No additional actions are required 
 - `0x1` Single user-mode:                  Boot into a basic shell without initializing AAG or AWM
 - `0x2` MAC EFI boot:                      A special type of boot that adds a sort of compatibility for MAC EFI firmware's, specifically it disables interrupts and all drivers that depends on interrupts
 - `0x3` Kernel Mode:                       It boot directly to the kernel without going to user mode, but still providing a filesystem and a basic shell 
 - `0x4` Headless Mode:                     Boots Atlas without anything happening on the screen
 - `0x5` BOOT DEBUG L1:                     Boots Atlas providing small messages of what is doing while booting
 - `0x6` BOOT DEBUG L2:                     Adds more information while booting
 - `0x7` BOOT DEBUG L3:                     Adds even more information while booting, so information that is annoying, specifically prints certain value


## Boot Operations Result

The BOR, also known as Boot Operations Result or is the kernel fucked up? is a variable initialized by the kernel and by the value of it, it tells the status after booting Atlas

BOR's:
 - `0x0` Boot succesfull:                   No issues or problems appeard
 - `0x1` Warnings happend:                  Some warnings happend while boot, but nothing critical
 - `0x2` Error on a driver:                 Error happend while initialization of a driver, but not that it can stop work
 - `0x3` Critical Error on a driver:        Critical error while initialization of a driver, faulty driver
 - `0x4` Aurora Faulty                      A component of Aurora didn't initialized correctly
 - `0x5` Initramfs Failed:                  Mounting the initramfs was failed                   
 - `0x6` Filesystem init failed             Should kernel panic
 - `0x7` ACPI Warning                       Possibly some ACPI and NON-ACPI tables weren't found.
 - `0x8` ACPI init Failed                   Should kernel panic
