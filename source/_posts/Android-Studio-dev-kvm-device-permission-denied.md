---
title: 'Android Studio: /dev/kvm device permission denied'
date: 2018-10-06 12:01:21
updated: 2018-10-06 12:01:21
tags: [Android, kvm]
categories: Programming
---

# 问题
&nbsp;&nbsp;Android Studio 报 Android Studio: /dev/kvm device permission denied 错误。

# 解决方案
>方案来自[stackoverflow](https://stackoverflow.com/questions/37300811/android-studio-dev-kvm-device-permission-denied)

&nbsp;&nbsp;As mentioned in the comments, starting with Ubuntu 18.04 and Linux Mint Tara you need to first
```
sudo apt install qemu-kvm.
```
To check the ownership of /dev/kvm use
```
ls -al /dev/kvm
```
The user was root, the group kvm. To check which users are in the kvm group, use
```
grep kvm /etc/group
```
This returned
```
kvm:x:some_number:
```
on my system: as there is nothing rightwards of the final :, there are no users in the kvm group.
To add the user yourname to the kvm group, you could use
```
sudo adduser yourname kvm
```
which adds the user to the group, and check once again with grep kvm /etc/group.

As mentioned by @Knossos, you might want to log out and back in (or restart), for the permissions to take effect.
