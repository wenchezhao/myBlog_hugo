---
title: "Ubuntu虚拟机镜像压缩"
date: 2020-12-31T21:29:55+08:00
images:
tags: 
  - Ubuntu、虚拟机
---

1. 把未使用的空间清零

   ```shell
   cat /dev/zero > zero.fill
   #sync
   sleep 1
   #sync
   rm -f zero.fill
   或者 
   cat /dev/zero > zero.fill;sync;sleep 1;sync;rm -f zero.fill
   ```

2. 使用vm的工具对压缩镜像

   ```shell
   vmware-vdiskmanager.exe -k "your.vmdk"
   ```

3. 更新虚拟机分配的磁盘大小

   ```shell
   vmware-vdiskmanager.exe -x ××GB "your.vmdk"
   ```

   

