# Known issues on Atlas

### Atlas Bootloader stuck at 'initializing pages'

Possibly a bootloader issue, happens on some system (like on a MacBook Air 2013 model)
when the built-in initramfs is too big.

### Atlas Bootloader stuck at 'love of the s*n' (Resolved)

Happens because the bootloader tries to allocate to memory the BootConfi, but the
BootConfig was not a pointer meaning that it corrupts the stack and crashes when
passed to the kernel entry point.

Fixed by making the BootConfig a pointer.

### Atlas Bootloader stuck at 'love os the s*n' when enabling interrupts (Resolved???)

Happens when enabling interrupts with 'asm ("sti");'.

Maybe this error is connected with the previous error?

### Noticeable glitches to the framebuffer and to AAG when unmasking the PIT bit

Happens when the PIT bit is unmasked, currently no idea why this happens.

### Atlas Bootloader stuck at memory mapping or a Panic with 'PFA OUT OF RESOURCES' (Resolved)

Happens when the EFI MEMORY DESCRIPTOR is corrupted or not initialized properly.

Fixed by correctly initializing the EFI MEMORY DESCRIPTOR.

### NON MASKABLE INTERRUPT when trying to force shutdown with power button

Happens on some systems (HP DESKTOP M01-Fxxxx) when pressing the power button
repetadly or long pressing.

### Black Screen when booting Atlas on a EFI based MacBook

Happens because a of a BootPanic but is not visible due to the TextMode not being
initialized.

### BootPanic with Error code 0x2

It happens when:
    - A file like 'aurora.elf', 'zap-vga16.psf' or 'atlas.bmp' is not found.
    - The root filesystem is not found.
    - Atlas is booted from another mass storage device.

Usually happens on EFI based MacBooks

### PS/2 mouse or keyboard not working properly on real-hardware

Seems to only happen on real-hardware, the possibly issue is that the PS/2
keyboard and mouse are not configured properly for that type of machines.

## STACK SEGMENT FAULT on mouse or keyboard interrupt

Again, mouse or keyboard interrupts not being configured properly.


