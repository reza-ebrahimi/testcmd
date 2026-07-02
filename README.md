# sudo mount /dev/sda2 /mnt/main
sudo mount --bind /dev /mnt/main/dev
sudo mount --bind /proc /mnt/main/proc
sudo mount --bind /sys /mnt/main/sys
sudo mount --bind /run /mnt/main/run
sudo mount /dev/sda3 /mnt/main/boot 2>/dev/null || true

sudo chroot /mnt/main

apt update
apt install --reinstall -y ubuntu-desktop dbus dbus-bin dbus-daemon dbus-user-session dbus-system-bus-common libdbus-1-3 gdm3 systemd

apt install --reinstall -y --fix-missing network-manager

update-initramfs -u -k all
update-grub

exit
sudo umount /mnt/main/dev /mnt/main/proc /mnt/main/sys /mnt/main/run /mnt/main/boot 2>/dev/null
sudo umount /mnt/main

reboot

----

dpkg --configure -a
apt install -f


