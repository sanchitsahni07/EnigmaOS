# EnigmaOS

A custom, Arch-based live and installable Linux ISO built with [archiso](https://wiki.archlinux.org/title/Archiso),
geared toward security work and daily use. It ships a Hyprland (Wayland) desktop and a
curated package set on top of a minimal Arch base.

## Features

- **Arch-based, built with archiso** — reproducible ISO builds from a declarative `profiledef.sh`.
- **Hyprland desktop** with supporting KDE/Plasma and Wayland utilities.
- **BIOS + UEFI boot** (syslinux for BIOS, GRUB for UEFI ia32/x64).
- **~900 packages** preinstalled, including networking and security tooling (e.g. `nmap`, `tcpdump`).
- **squashfs (xz) airootfs** for a compact live image.

## Build

Requires an Arch Linux host with `archiso` installed and root privileges:

```bash
sudo pacman -S archiso
sudo mkarchiso -v -w /tmp/enigma-work -o ./out .
```

The resulting ISO is written to `./out/`.

## Write to USB

```bash
sudo dd if=./out/EnigmaOS-*.iso of=/dev/sdX bs=4M status=progress oflag=sync
```

Replace `/dev/sdX` with your USB device. **This erases the target device — double-check it.**

## Repository layout

| Path | Purpose |
|------|---------|
| `profiledef.sh` | archiso profile definition (ISO name, boot modes, image options) |
| `packages.x86_64` | package list installed into the live system |
| `bootstrap_packages.x86_64` | packages for the bootstrap image |
| `pacman.conf` | pacman configuration used during the build |
| `airootfs/` | overlay filesystem (configs, skeleton files) copied into the live root |
| `efiboot/`, `grub/`, `syslinux/` | bootloader configuration for UEFI and BIOS |

## Author

Sanchit Sahni — https://github.com/0xpivot

## License

See repository for license terms.
