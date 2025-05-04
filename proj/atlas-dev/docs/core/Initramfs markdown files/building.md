# Building Atlas

The building system of Atlas is designed to be minimalistic and simple as possible without adding additional third-party resources

### Building ATLAS OS LOADER

The building can simply be done by cd into `gnu-efi/bootloader` and run `make bootloader`.

The EFI executable can be found in `gnu-efi/x86_64/bootloader`


### Building Aurora

First we need to prepare the initramfs.img, to do this cd into `kernel` and run `make initramfs`, this command will create a cpio newc archive in `kernel/bin` and `initramfs.h` inside `kernel/src`.

Then we actually compile the kernel with `make aurora`, the compiled kernel will be in `kernel/bin` named `aurora.elf`


### Make a image
`make buildimg` will create a image named `atlas-dev.img` in `kernel/bin`