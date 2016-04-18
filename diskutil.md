
# Disk Utility Tool Command Line

之前安裝 Ubuntu 的時候提到了 `dd` 命令，最近 Ubuntu 16.04 又爆出來引入了多款趙國生產的證書，因此我準備放棄虛擬機的 Kali，直接把 Ubuntu 換成 Kali，這時候就要發揮 `dd` 命令的作用了。

然而這篇我不準備寫 `dd` 命令，而是準備總結一下 OS X 系統下硬盤管理命令——Disk Utility。

## 簡單介紹

我在 Ubuntu 上試了一下，`apt-get` 並不能查到這個命令，而 OS X 系統下查了查 `diskutil` 命令類型，顯示說明它並不是系統原生命令，而是 OS X 特有的硬盤管理工具，配合有圖形界面，因此這個命令很有可能只在 OS X 系統下才有效。

```sh
$ diskutil -h
```

即可呼出命令幫助。

## 基礎命令行

下面是一些 `diskutil` 的常用命令行。

```sh
$ diskutil list     // list all disks
$ diskutil info     // show information about a specific disk
$ diskutil mount     // mount a volume
$ diskutil umout     // unmount a volume
$ diskutil eject     // eject a disk
```

## 其他常用命令

下面是一些或許會用到的命令行。

```sh
$ diskutil rename     // rename a volume
$ diskutil eraseDisk     // erase a disk
$ diskutil eraseVolume     // erase a volume
$ diskutil partitionDisk    // partition a disk, remove all volume
$ diskutil resizeVolume     // increase or decrease a volume's size
```

## 附錄：Dist Utility -h

Utility to manage local disks and volumes  
Most options require root access to the device

Usage:  diskutil [quiet] <verb> <options>, where <verb> is as follows:

     list                  (List the partitions of a disk)  
     info[rmation]         (Get information on a specific disk or partition)  
     listFilesystems       (List file systems available for formatting)  
     activity              (Continuous log of system-wide disk arbitration)  

     u[n]mount             (Unmount a single volume)  
     unmountDisk           (Unmount an entire disk (all volumes))   卸載硬盤  
     eject                 (Eject a disk)  
     mount                 (Mount a single volume)  
     mountDisk             (Mount an entire disk (all mountable volumes))   掛載硬盤  

     enableJournal         (Enable HFS+ journaling on a mounted HFS+ volume)  
     disableJournal        (Disable HFS+ journaling on a mounted HFS+ volume)  
     moveJournal           (Move the HFS+ journal onto another volume)  
     enableOwnership       (Treat as exact User/Group IDs for a mounted volume)  
     disableOwnership      (Ignore on-disk User/Group IDs for a mounted volume)  

     rename[Volume]        (Rename a volume)   重命名卷

     verifyVolume          (Verify the file system data structures of a volume)   驗證卷內文件數據結構    
     repairVolume          (Repair the file system data structures of a volume)   恢復卷內文件數據結構

     verifyDisk            (Verify the components of a partition map of a disk)   驗證硬盤分割區結構  
     repairDisk            (Repair the components of a partition map of a disk)   恢復硬盤分割區結構

     eraseDisk             (Erase an existing disk, removing all volumes)    格式化硬盤  
     eraseVolume           (Erase an existing volume)   格式化卷   
     reformat              (Erase an existing volume with same name and type)     
     eraseOptical          (Erase optical media (CD/RW, DVD/RW, etc.))   格式化特定媒體文件  
     zeroDisk              (Erase a disk, writing zeros to the media)  
     randomDisk            (Erase a disk, writing random data to the media)  
     secureErase           (Securely erase a disk or freespace on a volume)   安全格式化硬盤

     partitionDisk         ((re)Partition a disk, removing all volumes)   重新分割硬盤，刪除所有卷  
     resizeVolume          (Resize a volume, increasing or decreasing its size)   重新設置卷大小  
     splitPartition        (Split an existing partition into two or more)  
     mergePartitions       (Combine two or more existing partitions into one)  

     appleRAID <verb>      (Perform additional verbs related to AppleRAID)  
     coreStorage <verb>    (Perform additional verbs related to CoreStorage)  

diskutil <verb> with no options will provide help on that verb

