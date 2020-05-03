A collection of useful linux commands

Do not copy and paste anything in the shell without understanding it!

# General

# File management

## ls

Lists working directory content (current directory)

```console
ls
```

Enter a path to show the content of this path instead

```console
ls /path
```

Various options available. One in particular is -la

```console
ls -la /path
```

# Disks

## lsblk

Lists all available block devices (hard drives, usb sticks etc.) and shows their mounting points

```console
lsblk
```

## Write (iso) disk image to USB stick with progress

```console
dd if=/path/to/iso of=/dev/sdXY bs=4M status=progress
```

## mount

Mounts a partition to a existing directory

```console
mount /dev/sdXY /mnt/mountDir
```
`/dev/sdXY` = your partition path
`/mnt/mountPath` = your mount path

Required rights depend on the rights of the mount directory

The mount path can be any directory. /mnt/ is only an example.

## cryptsetup

Powerful tool to manage LUKS-encrypted devices.

### cryptsetup luksOpen

Opens a LUKS device (requires root rights):

```console
cryptsetup luksOpen /dev/sdXY luksName
```

`/dev/sdXY` = your device or partition path

`luksName` = your desired luks mapper name

The luks mapper will be available at `/dev/mapper/luksName`

### cryptsetup luksClose

Closes an open LUKS device

```console
cryptsetup luksClose luksName
```

`luksName` = luks mapper name

# Gnome-specific

## Restart gnome

Press `<Alt>F2`, then type `r`.

## nm-connection-editor

An advanced manager for network connections
```console
nm-connection-editor
```

## Change ALT+TAB behaviour (disable grouping windows by applications)
Open `dconf-editor`

Go to `org/gnome/desktop/wm/keybindings`

Move the value `'<Alt>Tab'` from `switch-applications` to `switch-windows`

Optionally move `'<Shift><Alt>Tab'` from `switch-applications-backward` to `switch-windows-backward`

If you want switch-windows to work across desktops, not just in the current desktop, you can also uncheck `org/gnome/shell/window-switcher/current-workspace-only`

Close `dconf-editor`

If using X11, press `<Alt>F2`, then type `r` to restart Gnome.

Credits to `Mad Physicist` and `CharlBotha`:

https://superuser.com/questions/394376/how-to-prevent-gnome-shells-alttab-from-grouping-windows-from-similar-apps

# Arch (Manjaro) specific

## Install VMware Player

### General installation instructions

https://wiki.manjaro.org/index.php?title=VMware

### Module compilation (on kernel 5.4, maybe others too)

```console
git clone https://github.com/mkubecek/vmware-host-modules.git
cd vmware-host-modules
git checkout workstation-15.5.1
sudo make
sudo make install

sudo vmware-modconfig --console --install-all
```

https://communities.vmware.com/thread/623768

https://github.com/mkubecek/vmware-host-modules

# Kubernetes

## Kubernetes Dashboard

### Access via remote ssh (e.g. terminal-only server)

Activate the web-ui access on the k8s machine
```console
kubectl proxy
```

Create SSH tunnel to the k8s machine
```console
ssh -L 8001:localhost:8001 user@remote-ip
```

Access web-ui via

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login

For older versions, use

http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#/login

# Proxmox

## Proxmox with systemd boot (used instead of grub for zfs boot)

### Editing kernel boot parameters

https://pve.proxmox.com/pve-docs/chapter-sysadmin.html#sysboot_edit_kernel_cmdline

## Image files location

```console
/var/lib/vz/images
```
