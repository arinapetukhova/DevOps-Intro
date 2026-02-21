# Lab 3 Submission
## Task 1: Operating System Analysis
### System Boot Time:
```
arina_os@arinaos:~$ systemd-analyze
systemd-analyze blame
Startup finished in 1.773s (kernel) + 2min 1.743s (userspace) = 2min 3.516s 
graphical.target reached after 2min 1.724s in userspace.
2min 43ms systemd-networkd-wait-online.service
   1.527s snapd.seeded.service
   1.483s snapd.service
    818ms NetworkManager.service
    447ms dev-mapper-ubuntu\x2d\x2dvg\x2dubuntu\x2d\x2dlv.device
    390ms dev-loop9.device
    387ms dev-loop10.device
    384ms dev-loop8.device
    328ms gnome-remote-desktop.service
    281ms power-profiles-daemon.service
    265ms polkit.service
    255ms NetworkManager-wait-online.service
    220ms snapd.apparmor.service
    218ms accounts-daemon.service
    216ms avahi-daemon.service
    208ms udisks2.service
    189ms secureboot-db.service
    183ms rsyslog.service
    165ms apparmor.service
    150ms grub-common.service
    148ms ModemManager.service
    146ms switcheroo-control.service
    143ms dev-loop3.device
    142ms dev-loop7.device
    141ms dev-loop4.device
    139ms dev-loop2.device
    137ms dev-loop5.device
    127ms dev-loop1.device
    126ms systemd-resolved.service
    125ms dev-loop6.device
    124ms apport.service
    120ms dbus.service
    119ms e2scrub_reap.service
    104ms pd-mapper.service
    102ms user@1000.service
     95ms systemd-networkd.service
     92ms systemd-oomd.service
     92ms dev-loop0.device
     82ms dev-mqueue.mount
     81ms sys-kernel-tracing.mount
     81ms sys-kernel-debug.mount
     80ms dev-hugepages.mount
     75ms keyboard-setup.service
     74ms kmod-static-nodes.service
     73ms lvm2-monitor.service
     71ms systemd-timesyncd.service
     69ms systemd-journald.service
     67ms modprobe@configfs.service
     65ms systemd-udev-trigger.service
     63ms systemd-journal-flush.service
     62ms systemd-logind.service
     62ms multipathd.service
     61ms upower.service
     60ms modprobe@drm.service
     59ms sysstat.service
     59ms systemd-udevd.service
     53ms modprobe@fuse.service
     49ms packagekit.service
     49ms geoclue.service
     47ms systemd-tmpfiles-setup.service
     47ms grub-initrd-fallback.service
     45ms systemd-fsck@dev-disk-by\x2duuid-b4d72888\x2d7ae9\x2d4e31\x2dae57\x2d>
     42ms wpa_supplicant.service
     42ms systemd-hostnamed.service
     42ms snap-bare-5.mount
     41ms gdm.service
     41ms systemd-modules-load.service
     39ms systemd-binfmt.service
     39ms snap-core22-1666.mount
     38ms snap-core22-1752.mount
     37ms systemd-tmpfiles-setup-dev-early.service
     37ms systemd-remount-fs.service
     35ms snap-firefox-4845.mount
     33ms boot.mount
     32ms snap-firefox-5698.mount
     31ms snap-gnome\x2d42\x2d2204-178.mount
     30ms cups.service
     29ms snap-gtk\x2dcommon\x2dthemes-1535.mount
     28ms sys-fs-fuse-connections.mount
     28ms systemd-localed.service
     28ms sys-kernel-config.mount
     27ms snap-snapd-21761.mount
     25ms colord.service
     25ms snap-snapd-25939.mount
     24ms systemd-fsck@dev-disk-by\x2duuid-CCB2\x2dE67C.service
     23ms swap.img.swap
     23ms kerneloops.service
     22ms snap-thunderbird-491.mount
     22ms systemd-random-seed.service
     22ms systemd-sysctl.service
     20ms snap-thunderbird-547.mount
     16ms plymouth-read-write.service
     16ms finalrd.service
     16ms console-setup.service
     14ms alsa-restore.service
     13ms lxd-installer.socket
      9ms proc-sys-fs-binfmt_misc.mount
      9ms ufw.service
      8ms user-runtime-dir@1000.service
      8ms systemd-update-utmp.service
      8ms snapd.socket
      7ms rtkit-daemon.service
      7ms systemd-user-sessions.service
      7ms boot-efi.mount
      7ms modprobe@dm_mod.service
      6ms spice-vdagentd.service
      6ms modprobe@efi_pstore.service
      5ms setvtrgb.service
      5ms modprobe@loop.service
      4ms openvpn.service
      4ms systemd-tmpfiles-setup-dev.service
      4ms plymouth-quit-wait.service
      3ms systemd-update-utmp-runlevel.service
     68us blk-availability.service
```
**Observations:** A total boot time of 2 minutes and 3 seconds was observed. The kernel was loaded in only 1.7 seconds, but the userspace took 2 minutes to start. The biggest delay was caused by `systemd-networkd-wait-online.service`, which waited 2 minutes for the network to be ready. The commands were run on a virtual machine, that's why the network was slower to initialize. Snap packages were also seen adding about 1.5 seconds to the boot process.

### System Load:
```
arina_os@arinaos:~$ uptime
w
 16:59:39 up 4 min,  1 user,  load average: 0.24, 0.18, 0.07
 16:59:39 up 4 min,  1 user,  load average: 0.24, 0.18, 0.07
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
arina_os tty2     -                16:57    4:12   0.01s  0.01s /usr/libexec/gn
```
**Observations:** The virtual machine was seen running for only 4 minutes after boot. Load averages of 0.24, 0.18, and 0.07 were displayed, which are very low numbers. This means the virtual CPU is not being heavily used. Only one user was found logged into the system through the graphical interface.

### Resource-Intensive Processes:
```
arina_os@arinaos:~$ ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head -n 6
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head -n 6
    PID    PPID CMD                         %MEM %CPU
   1841    1660 /usr/bin/gnome-shell         9.9  8.8
   2403    1841 /usr/libexec/mutter-x11-fra  2.1  0.1
   2320    1660 /usr/libexec/gsd-xsettings   1.8  0.1
   2276    1841 gjs /usr/share/gnome-shell/  1.5  0.3
   2414    1810 /usr/libexec/evolution-data  1.4  0.0
    PID    PPID CMD                         %MEM %CPU
   1841    1660 /usr/bin/gnome-shell         9.9  8.8
   2077    1955 /usr/libexec/ibus-extension  0.7  1.1
   2600    1660 /usr/libexec/gnome-terminal  1.2  1.0
      1       0 /sbin/init                   0.3  0.8
    798       1 /usr/lib/snapd/snapd         0.9  0.4
```
**Observations:** GNOME Shell was identified as the most resource-heavy process, with 9.9% of memory and 8.8% of CPU being used by it. This is expected because the desktop environment needs more resources to run the graphical interface in a virtual machine. Other processes like `mutter`, `ibus-extension`, and `gnome-terminal` were seen using very little memory and CPU. No signs of system struggle were noticed.

### Service Relationships:
```
arina_os@arinaos:~$ systemctl list-dependencies
systemctl list-dependencies multi-user.target
default.target
\u25cf \u251c\u2500accounts-daemon.service
\u25cf \u251c\u2500gdm.service
\u25cf \u251c\u2500gnome-remote-desktop.service
\u25cf \u251c\u2500power-profiles-daemon.service
\u25cf \u251c\u2500switcheroo-control.service
\u25cb \u251c\u2500systemd-update-utmp-runlevel.service
\u25cf \u251c\u2500udisks2.service
\u25cf \u2514\u2500multi-user.target
\u25cf   \u251c\u2500anacron.service
\u25cf   \u251c\u2500apport.service
\u25cf   \u251c\u2500avahi-daemon.service
\u25cf   \u251c\u2500console-setup.service
\u25cf   \u251c\u2500cron.service
\u25cf   \u251c\u2500cups-browsed.service
\u25cf   \u251c\u2500cups.path
\u25cf   \u251c\u2500cups.service
\u25cf   \u251c\u2500dbus.service
\u25cb   \u251c\u2500dmesg.service
\u25cb   \u251c\u2500e2scrub_reap.service
\u25cb   \u251c\u2500grub-common.service
\u25cb   \u251c\u2500grub-initrd-fallback.service
\u25cf   \u251c\u2500kerneloops.service
lines 1-23
```
**Observations:** A clear service hierarchy was shown: `default.target` was seen as the main goal that starts all graphical services like the login screen. Inside it, `multi-user.target` was found handling background services such as printing, scheduling, and error reporting. Active services were marked with black dots and inactive ones with white dots.

### Login Activity:
```
arina_os@arinaos:~$ who -a
last -n 5
           system boot  2026-02-20 16:55
LOGIN      ttyAMA0      2026-02-20 16:57              1144 id=AMA0
           run-level 5  2026-02-20 16:57
arina_os ? seat0        2026-02-20 16:57   ?          1722 (login screen)
arina_os + tty2         2026-02-20 16:57 00:08        1722 (tty2)
arina_os tty2         tty2             Fri Feb 20 16:57   still logged in
arina_os seat0        login screen     Fri Feb 20 16:57   still logged in
reboot   system boot  6.8.0-47-generic Fri Feb 20 16:55   still running
reboot   system boot  6.8.0-47-generic Fri Feb 20 16:53   still running
reboot   system boot  6.8.0-47-generic Fri Feb 20 16:51   still running

wtmp begins Wed Aug 28 08:25:05 2024
```
**Observations:** Three reboots were noticed at 16:51, 16:53, and 16:55, which were different attempts of starting the virtual machine. The current session was started at 16:55, and the user login was made at 16:57 through the graphical terminal. Only one user was found logged in.

### Memory Allocation:
```
arina_os@arinaos:~$ free -h
cat /proc/meminfo | grep -e MemTotal -e SwapTotal -e MemAvailable
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.0Gi       2.2Gi        57Mi       823Mi       2.8Gi
Swap:          3.8Gi          0B       3.8Gi
MemTotal:        3996336 kB
MemAvailable:    2953684 kB
SwapTotal:       3995644 kB
```
**Observations:** A total of 3.8 GB of RAM was seen allocated to the virtual machine. Only 1.0 GB of it was being used. Free memory of 2.2 GB was available, and 2.8 GB was shown as available for applications. Swap space of 3.8 GB was configured but no swap was being used because enough physical memory exists. About 823 MB was being used for cache to improve performance.

### Top Memory-Consuming Process:
GNOME Shell (PID: 1841) is the top memory-consuming process, using 9.9% of the system's total memory.

### Resource Utilization Patterns Observed:
A "single heavy user" pattern is visible where GNOME Shell (PID 1841) dominates both memory (9.9%) and CPU (8.8%), while all other processes use 2% or less of resources. A parent-child hierarchy exists with GNOME Shell spawning helper processes like `mutter-x11-fra` for window management and `gjs` for extensions. Background services such as `snapd` and `init` use minimal resources (under 1%), showing the system is well-optimized and not under any pressure despite being a virtual machine.

## Task 2: Networking Analysis
### Traceroute Execution:
```
arina_os@arinaos:~$ traceroute github.com
traceroute to github.com (140.82.121.4), 64 hops max
  1   192.168.64.1  1.146ms  0.524ms  0.535ms 
  2   10.91.48.1  6.109ms  4.793ms  6.397ms 
  3   10.252.6.1  5.820ms  5.107ms  8.373ms 
  4   188.170.164.34  8.542ms  9.917ms  10.533ms 
  5   *  *  * 
```

### DNS Resolution Check:
```
arina_os@arinaos:~$ dig github.com

; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> github.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 29388
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;github.com.			IN	A

;; ANSWER SECTION:
github.com.		17	IN	A	140.82.121.4

;; Query time: 18 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Sat Feb 21 14:32:13 UTC 2026
;; MSG SIZE  rcvd: 55
```

### Captured DNS Traffic:
```
arina_os@arinaos:~$ sudo tcpdump -c 5 -i any 'port 53' -nn
tcpdump: data link type LINUX_SLL2
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on any, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144 bytes
14:42:37.621513 lo    In  IP 127.0.0.1.36234 > 127.0.0.53.53: 48675+ [1au] A? google.com. (51)
14:42:37.622199 enp0s1 Out IP 192.168.64.2.38302 > 192.168.64.1.53: 32857+ [1au] A? google.com. (39)
14:42:37.637177 enp0s1 In  IP 192.168.64.1.53 > 192.168.64.2.38302: 32857 6/0/1 A 142.250.9.138, A 142.250.9.113, A 142.250.9.102, A 142.250.9.101, A 142.250.9.139, A 142.250.9.100 (135)
14:42:37.637565 lo    In  IP 127.0.0.53.53 > 127.0.0.1.36234: 48675 6/0/1 A 142.250.9.138, A 142.250.9.113, A 142.250.9.102, A 142.250.9.101, A 142.250.9.139, A 142.250.9.100 (135)
14:43:06.530191 lo    In  IP 127.0.0.1.45313 > 127.0.0.53.53: 20295+ A? microsoft.com. (31)
5 packets captured
18 packets received by filter
0 packets dropped by kernel
```

### PTR Lookups:
```
arina_os@arinaos:~$ dig -x 8.8.4.4
dig -x 1.1.2.2

; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 60460
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.		IN	PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.	4502	IN	PTR	dns.google.

;; Query time: 29 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Sat Feb 21 14:35:11 UTC 2026
;; MSG SIZE  rcvd: 73


; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> -x 1.1.2.2
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 54997
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;2.2.1.1.in-addr.arpa.		IN	PTR

;; AUTHORITY SECTION:
1.in-addr.arpa.		900	IN	SOA	ns.apnic.net. read-txt-record-of-zone-first-dns-admin.apnic.net. 23597 7200 1800 604800 3600

;; Query time: 29 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Sat Feb 21 14:35:11 UTC 2026
;; MSG SIZE  rcvd: 137
```

### Insights on Network Paths Discovered:
A traceroute to github.com was performed, and 4 successful hops were seen before the requests timed out. The first hop was identified as the local virtual machine gateway at `192.168.64.1`, and responses were received in under 1 millisecond. Private IP addresses (`10.x.x.x`) were used for the next two hops, which means they are part of the internet provider's internal network. Response times of 5-8 milliseconds were recorded for these hops. A public router at `188.170.164.34` was reached on the fourth hop, with response times between 8-10 milliseconds. Asterisks were shown for all probes after that. This does not mean github.com is unreachable - it just means the router at hop 5 is probably configured to ignore traceroute requests for security reasons.

### Analysis of DNS Query/Response Patterns:
A DNS query for github.com was performed using the `dig` command. A successful response with status NOERROR was received. The query was completed in only 18 milliseconds. The local Ubuntu resolver at `127.0.0.53` was used as the DNS server. This is systemd-resolved, which caches DNS results to improve speed. The IP address `140.82.121.4` was returned for github.com in the answer section. A TTL of 17 seconds was shown, which is quite short and indicates the address is changed frequently for load balancing purposes. Only one IP address was given in the response.

### Comparison of Reverse Lookup Results:
A reverse lookup was performed for `8.8.4.4`, and it was successful. The name "dns.google" was returned with a `NOERROR` status. This was expected because `8.8.4.4` is known to be one of Google's public DNS servers. A TTL of 4502 seconds (about 75 minutes) was shown. A reverse lookup was also performed for `1.1.2.2`, but a different result was received. An `NXDOMAIN` status was returned, which means no reverse record exists for this IP address. No answer section was provided, but an authority section with information from `APNIC` was shown instead. Both lookups took 29 milliseconds, so the resolver performance was consistent.

### Example DNS Query from Packet Capture:
One DNS query was captured when google.com was looked up. At 14:42:37, a packet was sent from the virtual machine. The source IP was `192.168.64.2` and the source port was `38302`. The destination IP was `192.168.64.1` and the destination port was `53`. An `A record` for google.com was being requested. The packet was marked as "Out", meaning it was leaving the computer through the `enp0s1 network interface`. A query ID of 32857 was used to match this request with its response later. The total size of the query was 39 bytes.