# On a Linux OS

1. find X:

  ```
  sudo fdisk -l
  sudo fdisk /dev/sdX
  ```

  1. partion /dev/sdX:

    ```
    Type o. This will clear out any partitions on the drive.
    Type p to list partitions. There should be no partitions left.
    Type n, then p for primary, 1 for the first partition on the drive, press ENTER to accept the default first sector, then type +100M for the last sector.
    Type t, then c to set the first partition to type W95 FAT32 (LBA).
    Type n, then p for primary, 2 for the second partition on the drive, and then press ENTER twice to accept the default first and last sector.
    Write the partition table and exit by typing w.
    ```

2. Create and mount filesystems:

  ```
  mkfs.vfat /dev/sdX1
  mkdir boot
  mount /dev/sdX1 boot
  mkfs.ext4 /dev/sdX2
  mkdir root
  mount /dev/sdX2 root
  ```

3. Download and extract the root filesystem (as root, not via sudo):

  ```
  sudo su
  wget http://archlinuxarm.org/os/ArchLinuxARM-rpi-2-latest.tar.gz
  bsdtar -xpf ArchLinuxARM-rpi-2-latest.tar.gz -C root
  sync
  ```

4. Move boot files to the first partition:

  ```
  mv root/boot/* boot
  ```

5. Unmount the two partitions:

  ```
  umount boot root
  ```
