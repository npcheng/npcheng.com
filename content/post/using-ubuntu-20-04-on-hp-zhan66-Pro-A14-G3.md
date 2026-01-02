---
title: 在hp_zhan66_Pro_A14_G3上安装配置ubuntu_20.04
date: 2020-11-07 19:21:09
tags:
---

HP 战66 AMD系列是农企在笔记本市场向INTEL发起反攻的产品，入手有小半年了，一直用的是默认的windows10操作系统。最经打算系统学习以下k8s，于是把计划把它升级一下。

战66本生支持双硬盘，双内存，有不错的扩展性。于是趁着内存条便宜，买了根8G 3200MHZ的kingston内存，掏出我多年多年未用的samsung硬盘全都安装上去。现在基本配置如下。

          *-cpu                     
            description: CPU
            product: AMD Ryzen 7 4700U with Radeon Graphics
            vendor: Advanced Micro Devices [AMD]
            physical id: 6
            bus info: cpu@0
            version: AMD Ryzen 7 4700U with Radeon Graphics
            serial: Unknown
            slot: FP6
            size: 4068MHz
            capacity: 4200MHz
            width: 64 bits
            clock: 100MHz

            *-disk                    
                description: ATA Disk
                product: Samsung SSD 850
                physical id: 0.0.0
                bus info: scsi@2:0.0.0
                logical name: /dev/sda
                version: 2B6Q
                serial: S2R7NB0J102009B
                size: 232GiB (250GB)

            Memory Device
                Array Handle: 0x0001
                Error Information Handle: 0x0007
                Total Width: 64 bits
                Data Width: 64 bits
                Size: 8192 MB
                Form Factor: SODIMM
                Set: None
                Locator: Bottom-Slot 1(left)
                Bank Locator: ChannelA0
                Type: DDR4
                Type Detail: Synchronous Unbuffered (Unregistered)
                Speed: 3200 MT/s
                Manufacturer: Kingston
                Serial Number: CFB9676B
                Asset Tag:  
            --
            Memory Device
                Array Handle: 0x0001
                Error Information Handle: 0x000B
                Total Width: 64 bits
                Data Width: 64 bits
                Size: 4096 MB
                Form Factor: SODIMM
                Set: None
                Locator: Bottom-Slot 2(right)
                Bank Locator: ChannelB0
                Type: DDR4
                Type Detail: Synchronous Unbuffered (Unregistered)
                Speed: 3200 MT/s
                Manufacturer: Micron
                Serial Number: 25FBCA3E
                Asset Tag:  

全程一路配置下来还算顺利。大致总结以下吧。

## 安装双系统
由于BIOS支持UEFI，装双系统轻松了很多。基本上网上的教程比较完备。推荐这一篇文章给大家。基本上不会出错

## 在ubuntu20.4下亮度调节失效

网上有好几种办法，其实与我的情况都不相符。但看内容大致上都是显卡问题引起的。因为显卡是集显，可以通过以下指令确认以下

    lshw -c video
    *-display                 
        description: VGA compatible controller
        product: Renoir
        vendor: Advanced Micro Devices, Inc. [AMD/ATI]
        physical id: 0
        bus info: pci@0000:05:00.0
        version: c2
        width: 64 bits
        clock: 33MHz
        capabilities: pm pciexpress msi msix vga_controller bus_master cap_list
        configuration: driver=amdgpu latency=0
        resources: irq:44 memory:d0000000-dfffffff memory:e0000000-e01fffff ioport:2000(size=256) memory:e0600000-e067ffff

在亮度调节未生效时， display被标识为（unclaim），也就是未识别。同时产看亮度调节文件目录，只用这个文件`sys/class/backlight/acpi_video0/brightness`,感觉到可能是因为CPU较新，可能驱动未更新。于是下载了最新的内核，内核下载页面在这里[https://kernel.ubuntu.com/~kernel-ppa/mainline/?C=N;O=D
][1]

    linux-headers-5.9.3-050903-generic_5.9.3-050903.202011011237_amd64.deb
    linux-image-unsigned-5.9.3-050903-generic_5.9.3-050903.202011011237_amd64.deb
    linux-modules-5.9.3-050903-generic_5.9.3-050903.202011011237_amd64.deb

然后运行`dpkg linux*.deb`,重启系统，遇到`has invalid signature`,别着急。修改BIOS中的secure boot， 将其关闭即可
重启后再查看 `/sys/class/backlight/` 目录多了个 `amdgpu_bl0`目录，原来的apci_video0没有了。亮度调节一切正常。

[1]: https://kernel.ubuntu.com/~kernel-ppa/mainline/?C=N;O=D
