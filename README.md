
# Void Linux Mac-Style Plymouth Theme

A custom Plymouth boot animation for Void Linux, inspired by the macOS boot animation. This theme uses the structure of the original Mac-Style Plymouth themes but features custom Void Linux branding and assets.

![Boot Animation Demo](void-mac-style.gif)

## Important Notes & Known Limitations

- **LUKS Encryption**: This theme works perfectly with LUKS full disk encryption. The password prompt will display correctly over the animation.
- **No Display Manager (DM)**: If you are booting directly into a TTY (i.e., not using a Display Manager like LightDM, SDDM, or GDM), Plymouth will not quit on its own. You will need to manually execute `plymouth --quit` using a method of your choice (e.g., adding it to your `.bash_profile`, `.zshrc`, or a custom startup script).
- **Poweroff & Reboot Animations**: Currently, this theme does not change the behavior of the poweroff and reboot animations. I have not done work in that regard yet, but I will probably do some research and add support for it in the future.

## Installation Guide

### 1. Install Plymouth
If you haven't already installed Plymouth on your Void Linux system, do so via `xbps`:
```bash
sudo xbps-install -S plymouth
```

### 2. Copy the theme files
Assuming you have cloned/downloaded the required files (`resources` and `void-mac-style.plymouth`), copy them to the Plymouth themes directory:
```bash
sudo cp -r void-mac-style/ /usr/share/plymouth/themes/
```
Make sure that the theme is present:
```bash
sudo plymouth-set-default-theme --list
```
Set the theme. The initramfs will be generated automatically, but if it doesn't, do it manually:
```bash
sudo plymouth-set-default-theme -R void-mac-style
```

### 3. Add "splash" to GRUB
To hide the boot text and show the Plymouth animation, you need to add the `splash` kernel parameter to your GRUB configuration.

1. Open your GRUB configuration file in your preferred text editor:
   ```bash
   sudo vim /etc/default/grub
   ```
2. Find the line starting with `GRUB_CMDLINE_LINUX_DEFAULT` and add `splash` to it. It should look something like this:
   ```bash
   GRUB_CMDLINE_LINUX_DEFAULT="loglevel=4 splash"
   ```
3. Update your GRUB configuration to apply the changes:
   ```bash
   sudo update-grub
   ```

### 4. Reboot
Reboot your system to enjoy your new Void Linux boot animation.

## Troubleshooting

- **Black screen or no animation**: Ensure `splash` is correctly added to `GRUB_CMDLINE_LINUX_DEFAULT` and that you have rebuilt both the initramfs (dracut) and GRUB (`update-grub`).
- **Plymouth doesn't disappear after boot**: As mentioned in the notes, if you are not using a Display Manager, Plymouth won't quit automatically. Run `plymouth --quit` or configure it to run automatically upon TTY login.

---

## Credits & Inspiration

- **Original Theme Structure & Inspiration**: Huge thanks to tobilinuxer for the original `linux-mac-style` Plymouth theme (and eren16 for the original base work). You can find the original project [here on GNOME-Look](https://www.gnome-look.org/p/2106821).
- **Custom Assets**: The official Void Linux logo and other graphical assets used in this theme are custom-made, but heavily inspired by the original creator's design and layout.
```


