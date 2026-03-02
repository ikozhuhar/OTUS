### ✅ Создание RAID-массива, Linux. Карманный справочник, стр. 216

```ruby
1. cat /proc/mdstat
2. sudo mdadm --create /dev/md1 --level 1 --raid-devices 2 /dev/sdb1 /dev/sdc1
3. cat /proc/mdstat
4. sudo mkfs.ext4 /dev/md1
5. sudo mount /dev/md1 /mnt/raid1/
6. df -h /mnt/raid1/
7. sudo mdadm --detail /dev/md1

# Когда массив будет готов, сохраните его конфигурацию, чтобы он монтировался автоматически при загрузке системы
1. sudo mdadm --detail --scan --verbose > /tmp/raid1
2. sudo mdadm --detail --scan --verbose >> /etc/mdadm/mdadm.conf
3. sudo update-initramfs -u
4. sudo reboot # для проверки, что RAID-массив сохранился
5. sudo echo "UUID=216dc813-feaa-49bb-966e-20e96ed4a6c7 /mnt/raid1 ext4 defaults 0 0" >> /etc/fstab
```


### Замена диска в RAID-массиве, Linux. Карманный справочник, стр. 219

```ruby
1. sudo cat /proc/mdstat
2. sudo mdadm --detail /dev/md1
3. sudo mdadm --manage /dev/md1 --fail /dev/sdf1
4. sudo mdadm --manage /dev/md1 --remove /dev/sdf1
5. sudo mdadm --manage /dev/md1 --add /dev/NEW1
6. sudo cat /proc/mdstat
```

### Удаление массива RAID, Linux. Карманный справочник, стр. 220

```ruby
1. sudo umount /mnt/raid
2. sudo mdadm --stop /dev/md1
3. sudo mdadm --zero-superblock /dev/sdg1 /dev/sdh1
4. Удалите из /etc/fstab и /etc/mdadm/mdadm.conf RAID массив /dev/md1 и сообщите об этом системе: sudo update-initramfs –u
5. sudo update-initramfs –u
```
