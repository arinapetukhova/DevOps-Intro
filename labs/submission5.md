# Lab 5 Submission
## Task 1: VirtualBox Installation
#### Host operating system and version:
macOS Tahoe 26.3
#### VirtualBox version number:
Version 7.2.6 r172322 (Qt6.8.0 on cocoa)

No installation issues were encountered.

## Task 2: Ubuntu VM and System Analysis
VirtualBox didn't work for me with Ubuntu 24.04, so I used UTM as a virtual machine instead.

**VM configuration:** 4GB RAM, 64GB storage, 4 CPU cores

### CPU Details:
**Tools discovered:** `lscpu`, `/proc/cpuinfo`, `nproc`

**Output:**
```
arina_os@arinaos:~$ lscpu
Architecture:             aarch64
  CPU op-mode(s):         64-bit
  Byte Order:             Little Endian
CPU(s):                   4
  On-line CPU(s) list:    0-3
Vendor ID:                Apple
  Model name:             -
    Model:                0
    Thread(s) per core:   1
    Core(s) per socket:   4
    Socket(s):            1
    Stepping:             0x0
    BogoMIPS:             48.00
    Flags:                fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fph
                          p asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 a
                          simddp sha512 asimdfhm dit uscat ilrcpc flagm sb paca 
                          pacg dcpodp flagm2 frint
NUMA:                     
  NUMA node(s):           1
  NUMA node0 CPU(s):      0-3
Vulnerabilities:          
  Gather data sampling:   Not affected
  Itlb multihit:          Not affected
  L1tf:                   Not affected
  Mds:                    Not affected
  Meltdown:               Not affected
  Mmio stale data:        Not affected
  Reg file data sampling: Not affected
  Retbleed:               Not affected
  Spec rstack overflow:   Not affected
  Spec store bypass:      Vulnerable
  Spectre v1:             Mitigation; __user pointer sanitization
  Spectre v2:             Not affected
  Srbds:                  Not affected
  Tsx async abort:        Not affected
arina_os@arinaos:~$ nproc
4
arina_os@arinaos:~$ cat /proc/cpuinfo
processor	: 0
BogoMIPS	: 48.00
Features	: fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 asimddp sha512 asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp flagm2 frint
CPU implementer	: 0x61
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0x000
CPU revision	: 0

processor	: 1
BogoMIPS	: 48.00
Features	: fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 asimddp sha512 asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp flagm2 frint
CPU implementer	: 0x61
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0x000
CPU revision	: 0

processor	: 2
BogoMIPS	: 48.00
Features	: fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 asimddp sha512 asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp flagm2 frint
CPU implementer	: 0x61
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0x000
CPU revision	: 0

processor	: 3
BogoMIPS	: 48.00
Features	: fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 asimddp sha512 asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp flagm2 frint
CPU implementer	: 0x61
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0x000
CPU revision	: 0
```

### Memory Information:
**Tools discovered:** `free`, `/proc/meminfo`, `vmstat`

**Output:**
```
arina_os@arinaos:~$ free
               total        used        free      shared  buff/cache   available
Mem:         3996340     1182244     1330892       55204     1700424     2814096
Swap:        3995644           0     3995644
arina_os@arinaos:~$ vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 0  0      0 1328936  52148 1648540    0    0  1742  1028  631    1  2  1 96  0  0  0
arina_os@arinaos:~$ cat /proc/meminfo
MemTotal:        3996340 kB
MemFree:         1328936 kB
MemAvailable:    2812492 kB
Buffers:           52156 kB
Cached:          1594424 kB
SwapCached:            0 kB
Active:          1447052 kB
Inactive:         908944 kB
Active(anon):     772056 kB
Inactive(anon):        0 kB
Active(file):     674996 kB
Inactive(file):   908944 kB
Unevictable:       46800 kB
Mlocked:           26240 kB
SwapTotal:       3995644 kB
SwapFree:        3995644 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:               308 kB
Writeback:             0 kB
AnonPages:        756216 kB
Mapped:           298088 kB
Shmem:             55200 kB
KReclaimable:      54184 kB
Slab:             168124 kB
SReclaimable:      54184 kB
SUnreclaim:       113940 kB
KernelStack:        9312 kB
ShadowCallStack:    2344 kB
PageTables:        17948 kB
SecPageTables:         0 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     5993812 kB
Committed_AS:    4763500 kB
VmallocTotal:   133141626880 kB
VmallocUsed:       29388 kB
VmallocChunk:          0 kB
Percpu:             2736 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB
ShmemHugePages:        0 kB
ShmemPmdMapped:        0 kB
FileHugePages:         0 kB
FilePmdMapped:         0 kB
CmaTotal:          32768 kB
CmaFree:           31104 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
Hugetlb:               0 kB
```

### Network Configuration:
**Tools discovered:** `ip`

**Output:**
```
arina_os@arinaos:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether ca:df:c5:b8:e1:3c brd ff:ff:ff:ff:ff:ff
    inet 192.168.64.2/24 brd 192.168.64.255 scope global dynamic noprefixroute enp0s1
       valid_lft 2888sec preferred_lft 2888sec
    inet6 fdd3:b293:e39d:89cf:3f86:a5a4:572a:2704/64 scope global temporary dynamic 
       valid_lft 604090sec preferred_lft 85440sec
    inet6 fdd3:b293:e39d:89cf:c8df:c5ff:feb8:e13c/64 scope global dynamic mngtmpaddr 
       valid_lft 2591952sec preferred_lft 604752sec
    inet6 fe80::c8df:c5ff:feb8:e13c/64 scope link 
       valid_lft forever preferred_lft forever
```

### Storage Information:
**Tools discovered:** `df`, `lsblk`

**Output:**
```
arina_os@arinaos:~$ df
Filesystem                        1K-blocks     Used Available Use% Mounted on
tmpfs                                399636     1860    397776   1% /run
efivarfs                                256       28       229  11% /sys/firmware/efi/efivars
/dev/mapper/ubuntu--vg-ubuntu--lv  31270768 13499804  16156936  46% /
tmpfs                               1998168        0   1998168   0% /dev/shm
tmpfs                                  5120        8      5112   1% /run/lock
/dev/vda2                           1992552   206600   1664712  12% /boot
/dev/vda1                           1098628     6508   1092120   1% /boot/efi
tmpfs                                399632      128    399504   1% /run/user/1000
arina_os@arinaos:~$ lsblk
NAME                      MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0                       7:0    0     4K  1 loop /snap/bare/5
loop1                       7:1    0  68.8M  1 loop /snap/core22/1666
loop2                       7:2    0  68.8M  1 loop /snap/core22/1752
loop4                       7:4    0 234.9M  1 loop /snap/firefox/5698
loop5                       7:5    0 483.3M  1 loop /snap/gnome-42-2204/178
loop6                       7:6    0  91.7M  1 loop /snap/gtk-common-themes/1535
loop7                       7:7    0  33.7M  1 loop /snap/snapd/21761
loop8                       7:8    0  41.6M  1 loop /snap/snapd/25939
loop9                       7:9    0   240M  1 loop /snap/firefox/7897
loop10                      7:10   0 219.2M  1 loop /snap/thunderbird/958
loop11                      7:11   0   220M  1 loop /snap/thunderbird/994
sr0                        11:0    1  1024M  0 rom  
vda                       253:0    0    64G  0 disk 
\u251c\u2500vda1                    253:1    0     1G  0 part /boot/efi
\u251c\u2500vda2                    253:2    0     2G  0 part /boot
\u2514\u2500vda3                    253:3    0  60.9G  0 part 
  \u2514\u2500ubuntu--vg-ubuntu--lv 252:0    0  30.5G  0 lvm  /
```

### Operating System:
**Tools discovered:** `uname`, `hostnamectl`

**Output:**
```
arina_os@arinaos:~$ uname
Linux
arina_os@arinaos:~$ hostnamectl
 Static hostname: arinaos
       Icon name: computer-vm
         Chassis: vm \U0001f5b4
      Machine ID: d9d987f1ef9342639b1d58d683bcc891
         Boot ID: 2df7d21fa56b432ba7f1b43b8595aff4
  Virtualization: qemu
Operating System: Ubuntu 24.04 LTS                
          Kernel: Linux 6.8.0-47-generic
    Architecture: arm64
 Hardware Vendor: QEMU
  Hardware Model: QEMU Virtual Machine
Firmware Version: 0.0.0
   Firmware Date: Fri 2015-02-06
    Firmware Age: 11y 3w 1d         
```

### Virtualization Detection:
**Tools discovered:** `systemd-detect-virt`, `lshw`

**Output:**
```
arina_os@arinaos:~$ lshw
WARNING: you should run this program as super-user.
arinaos                     
    description: Computer
    width: 64 bits
    capabilities: smp cp15_barrier swp tagged_addr_disabled
  *-core
       description: Motherboard
       physical id: 0
     *-memory
          description: System memory
          physical id: 0
          size: 4GiB
     *-cpu:0
          physical id: 1
          bus info: cpu@0
          capabilities: fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 asimddp sha512 asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp flagm2 frint
     *-cpu:1
          physical id: 2
          bus info: cpu@1
          capabilities: fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 asimddp sha512 asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp flagm2 frint
     *-cpu:2
          physical id: 3
          bus info: cpu@2
          capabilities: fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 asimddp sha512 asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp flagm2 frint
     *-cpu:3
          physical id: 4
          bus info: cpu@3
          capabilities: fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 asimddp sha512 asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp flagm2 frint
     *-pci
          description: Host bridge
          product: QEMU PCIe Host bridge
          vendor: Red Hat, Inc.
          physical id: 100
          bus info: pci@0000:00:00.0
          version: 00
          width: 32 bits
          clock: 33MHz
        *-network
             description: Ethernet controller
             product: Virtio network device
             vendor: Red Hat, Inc.
             physical id: 1
             bus info: pci@0000:00:01.0
             version: 00
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list rom
             configuration: driver=virtio-pci latency=0
             resources: irq:46 ioport:10c0(size=32) memory:10060000-10060fff memory:10040000-10043fff memory:10000000-1003ffff
           *-virtio0
                description: Ethernet interface
                physical id: 0
                bus info: virtio@0
                logical name: enp0s1
                serial: ca:df:c5:b8:e1:3c
                capabilities: ethernet physical
                configuration: autonegotiation=off broadcast=yes driver=virtio_net driverversion=1.0.0 ip=192.168.64.2 link=yes multicast=yes
        *-display
             description: Display controller
             product: Virtio 1.0 GPU
             vendor: Red Hat, Inc.
             physical id: 2
             bus info: pci@0000:00:02.0
             logical name: /dev/fb0
             version: 01
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list fb
             configuration: depth=32 driver=virtio-pci latency=0 resolution=1280,800
             resources: irq:47 memory:10061000-10061fff memory:10044000-10047fff
           *-virtio1 UNCLAIMED
                description: Virtual I/O device
                physical id: 0
                bus info: virtio@1
                configuration: driver=virtio_gpu
        *-multimedia
             description: Audio device
             product: 82801FB/FBM/FR/FW/FRW (ICH6 Family) High Definition Audio Controller
             vendor: Intel Corporation
             physical id: 3
             bus info: pci@0000:00:03.0
             logical name: card0
             logical name: /dev/snd/controlC0
             logical name: /dev/snd/hwC0D0
             logical name: /dev/snd/pcmC0D0c
             logical name: /dev/snd/pcmC0D0p
             version: 01
             width: 32 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=snd_hda_intel latency=0
             resources: irq:76 memory:10048000-1004bfff
        *-usb:0
             description: USB controller
             product: uPD720200 USB 3.0 Host Controller
             vendor: NEC Corporation
             physical id: 4
             bus info: pci@0000:00:04.0
             version: 03
             width: 64 bits
             clock: 33MHz
             capabilities: xhci bus_master cap_list
             configuration: driver=xhci_hcd latency=0
             resources: irq:45 memory:1004c000-1004ffff
        *-usb:1
             description: USB controller
             product: QEMU XHCI Host Controller
             vendor: Red Hat, Inc.
             physical id: 5
             bus info: pci@0000:00:05.0
             version: 01
             width: 64 bits
             clock: 33MHz
             capabilities: xhci bus_master cap_list
             configuration: driver=xhci_hcd latency=0
             resources: irq:46 memory:10050000-10053fff
        *-scsi
             description: SCSI storage controller
             product: Virtio block device
             vendor: Red Hat, Inc.
             physical id: 6
             bus info: pci@0000:00:06.0
             version: 00
             width: 64 bits
             clock: 33MHz
             capabilities: scsi bus_master cap_list
             configuration: driver=virtio-pci latency=0
             resources: irq:47 ioport:1000(size=128) memory:10062000-10062fff memory:10054000-10057fff
           *-virtio2
                description: Virtual I/O device
                physical id: 0
                bus info: virtio@2
                logical name: /dev/vda
                configuration: driver=virtio_blk
        *-communication
             description: Communication controller
             product: Virtio console
             vendor: Red Hat, Inc.
             physical id: 7
             bus info: pci@0000:00:07.0
             version: 00
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=virtio-pci latency=0
             resources: irq:48 ioport:1080(size=64) memory:10063000-10063fff memory:10058000-1005bfff
           *-virtio3 UNCLAIMED
                description: Virtual I/O device
                physical id: 0
                bus info: virtio@3
                configuration: driver=virtio_console
        *-generic
             description: Unclassified device
             product: Virtio RNG
             vendor: Red Hat, Inc.
             physical id: 8
             bus info: pci@0000:00:08.0
             version: 00
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=virtio-pci latency=0
             resources: irq:45 ioport:10e0(size=32) memory:10064000-10064fff memory:1005c000-1005ffff
           *-virtio4 UNCLAIMED
                description: Virtual I/O device
                physical id: 0
                bus info: virtio@4
                configuration: driver=virtio_rng
     *-pnp00:00
          product: PnP device PNP0c02
          physical id: 5
          capabilities: pnp
          configuration: driver=system
     *-scsi
          physical id: 6
          bus info: usb@1:4.1
          logical name: scsi0
          capabilities: emulated scsi-host
          configuration: driver=usb-storage
        *-cdrom
             description: DVD reader
             product: QEMU CD-ROM
             vendor: QEMU
             physical id: 0.0.0
             bus info: scsi@0:0.0.0
             logical name: /dev/cdrom
             logical name: /dev/sr0
             version: 2.5+
             capabilities: removable audio dvd
             configuration: ansiversion=5 status=nodisc
  *-input:0
       product: Power Button
       physical id: 1
       logical name: input0
       logical name: /dev/input/event0
       capabilities: platform
  *-input:1
       product: QEMU QEMU USB Tablet
       physical id: 2
       logical name: input1
       logical name: /dev/input/event1
       logical name: /dev/input/mouse0
       capabilities: usb
  *-input:2
       product: QEMU QEMU USB Mouse
       physical id: 3
       logical name: input2
       logical name: /dev/input/event2
       logical name: /dev/input/mouse1
       capabilities: usb
  *-input:3
       product: QEMU QEMU USB Keyboard
       physical id: 4
       logical name: input3
       logical name: /dev/input/event3
       logical name: input3::capslock
       logical name: input3::compose
       logical name: input3::kana
       logical name: input3::numlock
       logical name: input3::scrolllock
       capabilities: usb
  *-input:4
       product: spice vdagent tablet
       physical id: 5
       logical name: input6
       logical name: /dev/input/event4
       logical name: /dev/input/js0
       logical name: /dev/input/mouse2
WARNING: output may be incomplete or inaccurate, you should run this program as super-user.
arina_os@arinaos:~$ systemd-detect-virt
qemu
```

#### Reflection on the most useful tools:
`lscpu` gives CPU architecture, core count, vendor, and security status in one clean output, which is faster than parsing `/proc/cpuinfo`.

`free -h` shows total and available RAM in human-readable form compared to `/proc/meminfo`.

`lsblk` displays disk partitions in a tree format. It clearly shows the 64GB disk split into EFI, boot, and LVM volumes—information hard to get from `df` alone.

`ip a` quickly lists network interfaces and IP addresses. It confirmed the active interface `enp0s1` with IP `192.168.64.2` on a DHCP network.

`hostnamectl` replaces multiple commands by showing OS version, kernel, and virtualization type all at once.
