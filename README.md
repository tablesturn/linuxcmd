A collection of useful linux commands

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
