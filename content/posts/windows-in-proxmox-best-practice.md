---
title: "Windows OS in Proxmox - VM Settings Best Practice"
date: 2022-10-07T17:42:29-04:00
slug: 2022-10-07-windows-in-proxmox-best-practice
type: posts
draft: false
categories:
  - How-To
tags:
  - proxmox
  - windows
---

After struggling with performance and driver issues with Windows operating systems on Proxmox, I came across some documentation that made things a lot easier. Here are some of the articles on their wiki:

[Windows 2022 guest best practices](https://pve.proxmox.com/wiki/Windows_2022_guest_best_practices)
<br>[Windows 2019 guest best practices](https://pve.proxmox.com/wiki/Windows_2019_guest_best_practices)
<br>[Windows 10 guest best practices](https://pve.proxmox.com/wiki/Windows_10_guest_best_practices)

These are the settings that I now use for Windows VMs in Proxmox.

* Guest OS: Microsoft Windows
* Version: 10/2016/2019
* SCSO Controller: VirtIO SCSI
* Qemu Agent: Enabled
* Cache: Default (safer but slower)
      <br>*Optional for performance: "Write back"*
* Discard: Enabled (TRIM)
* NIC Model: VirtIO (paravirtualized)
* [Latest stable VirtIO Drivers](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso)