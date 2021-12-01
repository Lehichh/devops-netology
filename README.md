# devops-netology
**Sarkisyan Aleksey**

**Выполнение задания 3.5 FS**


**1.**

Ознакомился.


**2.**

Нет не могут, они имеют ту же информацию inode и набор разрешений что и у исходного файла.


**3.**

Готово.

https://yapx.ru/v/PWCWe


**4.**

**sudo fdisk /dev/sdb** далее в интерактивном режиме задаем параметры

https://yapx.ru/v/PWCoe


**5.**

**sudo sfdisk -d /dev/sdb| sudo sfdisk /dev/sdc**

https://yapx.ru/v/PWCfV


**6.**

**sudo mdadm --create --verbose /dev/md0 -l 1 -n 2 /dev/sd{b1,c1}**

https://yapx.ru/v/PWCUq


**7.**

**sudo mdadm --create --verbose /dev/md1 -l 0 -n 2 /dev/sd{b2,c2}**

https://yapx.ru/v/PWCRz


**8.**

две команды **sudo pvcreate /dev/md0** и **sudo pvcreate /dev/md1**, можно так же одной командой через пробел прописать md-устройства 

https://yapx.ru/v/PWCKO


**9.**

**sudo vgcreate vol_grp1 /dev/md0 /dev/md1**

https://yapx.ru/v/PWFZH


**10.**

**sudo lvcreate -n diskfortest -L 100M vol_grp1 /dev/md1**

https://yapx.ru/v/PWPQF


**11.**

готово.

vagrant@vagrant:~$ sudo mkfs.ext4 /dev/vol_grp1/diskfortest

mke2fs 1.45.5 (07-Jan-2020)

Creating filesystem with 25600 4k blocks and 25600 inodes


Allocating group tables: done

Writing inode tables: done

Creating journal (1024 blocks): done

Writing superblocks and filesystem accounting information: done


**12.**

**mount /dev/vol_grp1/diskfortest /tmp/new**


**13.**

Выполнил.


**14.**

https://yapx.ru/v/PWQod


**15.**

Простестировал.

**root@vagrant:~# gzip -t /tmp/new/test.gz**

**root@vagrant:~# echo $?**

**0**


**16.**

https://yapx.ru/v/PWS33


**17.**

https://yapx.ru/v/PWVN0


**18.**

https://yapx.ru/v/PWVVu


**19.**

Так как у нас RAID1 - зеркало, то и тесть без ошибок

https://yapx.ru/v/PWVaP


**20.**

Выполнил.