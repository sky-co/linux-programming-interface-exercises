Chapter 12: System and Process Information
==========================================

Exercise 12-1
-------------

**Question**

Write a program that lists the porcess ID and command name for all
processes being run by the user named in the program's command-line
argument.  (You may find the userIdFromName() function from Listing
8-1, on page 159, useful.)  This can be done by inspecting the Name:
and Uid: lines of all of the /proc/PID/status files on the system.
Walking through all of the /proc/PID directories on the system
requires the use of readdir(3), which is described in Section 18.8.
Make sure your porgram correctly handles the possibility that a
/proc/PID directory disappears between the time that the porgram
determines that the directory exists and the time that it tries to
open the corresponding /proc/PID/status file.

**Answer**

See proclist.c.  Example Output:

```
[posborne@pobox-lin:~/Projects/linux-programming-interface-exercises/ch12 git:master] $ ./prog_proclist posborne
22548: prog_proclist
1105: chrome
1115: chrome
1325: chrome
1658: mate-session
1693: ssh-agent
1696: dbus-launch
1697: dbus-daemon
1704: mateconfd-2
1708: mate-keyring-da
1716: mate-settings-d
1720: gvfsd
1722: gvfs-fuse-daemo
1733: gvfs-gdu-volume
1743: gvfs-afc-volume
1746: gvfs-gphoto2-vo
1751: mate-panel
1754: caja
1758: mate-power-mana
1759: deja-dup-monito
1762: zeitgeist-datah
1767: matecomponent-a
1769: mate-bluetooth-
1775: polkit-mate-aut
1776: nm-applet
1787: zeitgeist-daemo
1790: mate-settings-d
1791: gnome-do
1793: mate-settings-d
1798: update-notifier
1805: zeitgeist-fts
1813: applet.py
1820: wnck-applet
1822: pulseaudio
1830: mate-screensave
1833: clock-applet
1835: multiload-apple
1837: notification-ar
1855: gnome-do
2023: cat
2026: gvfsd-trash
2033: gconfd-2
2054: gconf-helper
2085: gvfsd-metadata
2105: chrome
2112: chrome
2113: chrome-sandbox
2114: chrome
2116: nacl_helper_boo
2117: chrome
2153: chrome
2204: chrome
2217: chrome
2316: at-spi-bus-laun
2592: mixer_applet2
2704: chrome
2811: chrome
2835: chrome
2845: chrome
2869: chrome
2892: chrome
2908: chrome
2932: emacs
2936: chrome
2949: chrome
2961: chrome
2968: chrome
2989: chrome
3202: notify-osd
3210: dconf-service
7241: chrome
7833: chrome
10392: eclipse
10463: java
12447: chrome
14552: firefox
14587: plugin-containe
14721: mate-terminal
14727: mate-terminal
14728: bash
19678: marco
19691: chrome
19794: chrome
19898: chrome
19909: chrome
19939: chrome
19960: chrome
19979: chrome
20035: chrome
20107: chrome
20519: chrome
20706: emacsclient
22548: prog_proclist
```

Exercise 12-2
-------------

**Question**

Write a program that draws a tree showing the hierarchical
parent-child relationships of all processes on the system, going all
the way back to init.  For each process, the program should display
the process ID and the command being executed.  The output of the
program should be similar to that produced by pstree(1), although it
does need not to be as sophisticated.  The parent of each process on
the system can be found by inspecing the PPid: line of all of the
/proc/PID/status files on the system.  Be careful to handle the
possibilty that a process's parent (and thus its /proc/PID directory)
disappears during the scan of all /proc/PID directories.

**Answer**

See pstree.c.  Example output:

```
[posborne@pobox-lin:~/Projects/linux-programming-interface-exercises/ch12
git:master] $ ./prog_pstree
kthreadd (pid: 2, ppid: 0)
  kworker/0 (pid: 23815, ppid: 2)
  kworker/3 (pid: 23695, ppid: 2)
  kworker/0 (pid: 23603, ppid: 2)
  kworker/1 (pid: 23453, ppid: 2)
  krfcommd (pid: 1054, ppid: 2)
  flush-8 (pid: 944, ppid: 2)
  hd-audio1 (pid: 805, ppid: 2)
  hd-audio0 (pid: 801, ppid: 2)
  edac-poller (pid: 746, ppid: 2)
  ext4-dio-unwrit (pid: 312, ppid: 2)
  jbd2/sdb5-8 (pid: 311, ppid: 2)
  scsi_eh_5 (pid: 292, ppid: 2)
  scsi_eh_4 (pid: 290, ppid: 2)
  firewire (pid: 270, ppid: 2)
  devfreq_wq (pid: 121, ppid: 2)
  kworker/u (pid: 92, ppid: 2)
  kworker/u (pid: 90, ppid: 2)
  scsi_eh_3 (pid: 88, ppid: 2)
  scsi_eh_2 (pid: 87, ppid: 2)
  scsi_eh_1 (pid: 86, ppid: 2)
  scsi_eh_0 (pid: 85, ppid: 2)
  kthrotld (pid: 77, ppid: 2)
  crypto (pid: 69, ppid: 2)
  ecryptfs-kthrea (pid: 68, ppid: 2)
  fsnotify_mark (pid: 67, ppid: 2)
  khugepaged (pid: 66, ppid: 2)
  ksmd (pid: 65, ppid: 2)
  kswapd0 (pid: 64, ppid: 2)
  khungtaskd (pid: 63, ppid: 2)
  md (pid: 32, ppid: 2)
  khubd (pid: 31, ppid: 2)
  ata_sff (pid: 30, ppid: 2)
  kblockd (pid: 29, ppid: 2)
  kintegrityd (pid: 28, ppid: 2)
  bdi-default (pid: 27, ppid: 2)
  sync_supers (pid: 26, ppid: 2)
  netns (pid: 24, ppid: 2)
  kdevtmpfs (pid: 23, ppid: 2)
  khelper (pid: 22, ppid: 2)
  cpuset (pid: 21, ppid: 2)
  watchdog/3 (pid: 20, ppid: 2)
  ksoftirqd/3 (pid: 19, ppid: 2)
  kworker/3 (pid: 18, ppid: 2)
  migration/3 (pid: 17, ppid: 2)
  watchdog/2 (pid: 16, ppid: 2)
  ksoftirqd/2 (pid: 15, ppid: 2)
  migration/2 (pid: 13, ppid: 2)
  watchdog/1 (pid: 12, ppid: 2)
  ksoftirqd/1 (pid: 10, ppid: 2)
  migration/1 (pid: 8, ppid: 2)
  watchdog/0 (pid: 7, ppid: 2)
  migration/0 (pid: 6, ppid: 2)
  ksoftirqd/0 (pid: 3, ppid: 2)
init (pid: 1, ppid: 0)
  mate-terminal (pid: 14721, ppid: 1)
    mate-terminal (pid: 14727, ppid: 14721)
  firefox (pid: 14552, ppid: 1)
  eclipse (pid: 10392, ppid: 1)
  dconf-service (pid: 3210, ppid: 1)
  notify-osd (pid: 3202, ppid: 1)
  emacs (pid: 2932, ppid: 1)
  mixer_applet2 (pid: 2592, ppid: 1)
  hald (pid: 2454, ppid: 1)
  at-spi-bus-laun (pid: 2316, ppid: 1)
  chrome (pid: 2105, ppid: 1)
    chrome-sandbox (pid: 2113, ppid: 2105)
    chrome (pid: 2112, ppid: 2105)
  system-service- (pid: 2087, ppid: 1)
  gvfsd-metadata (pid: 2085, ppid: 1)
  SystemToolsBack (pid: 2070, ppid: 1)
  system-tools-ba (pid: 2044, ppid: 1)
  gconfd-2 (pid: 2033, ppid: 1)
  gvfsd-trash (pid: 2026, ppid: 1)
  notification-ar (pid: 1837, ppid: 1)
  multiload-apple (pid: 1835, ppid: 1)
  clock-applet (pid: 1833, ppid: 1)
  mate-screensave (pid: 1830, ppid: 1)
  upowerd (pid: 1829, ppid: 1)
  rtkit-daemon (pid: 1824, ppid: 1)
  pulseaudio (pid: 1822, ppid: 1)
  wnck-applet (pid: 1820, ppid: 1)
  zeitgeist-fts (pid: 1805, ppid: 1)
  zeitgeist-daemo (pid: 1787, ppid: 1)
  matecomponent-a (pid: 1767, ppid: 1)
  gvfs-gphoto2-vo (pid: 1746, ppid: 1)
  gvfs-afc-volume (pid: 1743, ppid: 1)
  udisks-daemon (pid: 1735, ppid: 1)
  gvfs-gdu-volume (pid: 1733, ppid: 1)
  gvfs-fuse-daemo (pid: 1722, ppid: 1)
  gvfsd (pid: 1720, ppid: 1)
  mate-keyring-da (pid: 1708, ppid: 1)
  mateconfd-2 (pid: 1704, ppid: 1)
  dbus-daemon (pid: 1697, ppid: 1)
  dbus-launch (pid: 1696, ppid: 1)
  console-kit-dae (pid: 1583, ppid: 1)
  accounts-daemon (pid: 1560, ppid: 1)
  getty (pid: 1515, ppid: 1)
  hddtemp (pid: 1280, ppid: 1)
  whoopsie (pid: 1132, ppid: 1)
  polkitd (pid: 1118, ppid: 1)
  atd (pid: 1114, ppid: 1)
  irqbalance (pid: 1112, ppid: 1)
  cron (pid: 1111, ppid: 1)
  lightdm (pid: 1102, ppid: 1)
    lightdm (pid: 22010, ppid: 1102)
    lightdm (pid: 21029, ppid: 1102)
    lightdm (pid: 1555, ppid: 1102)
    Xorg (pid: 1146, ppid: 1102)
  avahi-daemon (pid: 1100, ppid: 1)
  acpid (pid: 1099, ppid: 1)
  getty (pid: 1094, ppid: 1)
  getty (pid: 1092, ppid: 1)
  getty (pid: 1091, ppid: 1)
  colord (pid: 1089, ppid: 1)
  getty (pid: 1075, ppid: 1)
  NetworkManager (pid: 1070, ppid: 1)
    dhclient (pid: 1148, ppid: 1070)
  getty (pid: 1061, ppid: 1)
  bluetoothd (pid: 1039, ppid: 1)
  cupsd (pid: 1023, ppid: 1)
  modem-manager (pid: 996, ppid: 1)
  dbus-daemon (pid: 970, ppid: 1)
  rsyslogd (pid: 923, ppid: 1)
  mount.ntfs (pid: 870, ppid: 1)
  mount.ntfs (pid: 833, ppid: 1)
  upstart-socket- (pid: 824, ppid: 1)
  udevd (pid: 515, ppid: 1)
    udevd (pid: 1499, ppid: 515)
  upstart-udev-br (pid: 508, ppid: 1)
```

Exercise 12-3
-------------

**Question**

Write a program that lists all processes that have a particular file
pathname open.  This can be achieved by inspecting the contents of all
of the /proc/PID/fd/* symbolic links.  This will require nested loops
employing readdir(3) to scan all /proc/PID directories, and then the
contents of all /proc/PID/fd entries within each /proc/PID directory.
To read the contents of a /proc/PID/fd/n symbolic link requires the
use of readlink(), described in Section 18.5.

**Answer**

See sherlock.c (haha, clever)...

Example output:

```
Processes with handles to "/dev/null":
mate-session (pid: 1658)
dbus-launch (pid: 1696)
dbus-daemon (pid: 1697)
mateconfd-2 (pid: 1704)
mate-keyring-da (pid: 1708)
mate-settings-d (pid: 1716)
gvfsd (pid: 1720)
gvfs-fuse-daemo (pid: 1722)
gvfs-gdu-volume (pid: 1733)
gvfs-afc-volume (pid: 1743)
gvfs-gphoto2-vo (pid: 1746)
mate-panel (pid: 1751)
caja (pid: 1754)
mate-power-mana (pid: 1758)
deja-dup-monito (pid: 1759)
zeitgeist-datah (pid: 1762)
matecomponent-a (pid: 1767)
mate-bluetooth- (pid: 1769)
polkit-mate-aut (pid: 1775)
nm-applet (pid: 1776)
zeitgeist-daemo (pid: 1787)
mate-settings-d (pid: 1790)
gnome-do (pid: 1791)
mate-settings-d (pid: 1793)
update-notifier (pid: 1798)
zeitgeist-fts (pid: 1805)
applet.py (pid: 1813)
wnck-applet (pid: 1820)
pulseaudio (pid: 1822)
mate-screensave (pid: 1830)
clock-applet (pid: 1833)
multiload-apple (pid: 1835)
notification-ar (pid: 1837)
gnome-do (pid: 1855)
gvfsd-trash (pid: 2026)
gconfd-2 (pid: 2033)
gconf-helper (pid: 2054)
gvfsd-metadata (pid: 2085)
chrome (pid: 2105)
chrome (pid: 2112)
chrome (pid: 2114)
nacl_helper_boo (pid: 2116)
chrome (pid: 2217)
at-spi-bus-laun (pid: 2316)
mixer_applet2 (pid: 2592)
emacs (pid: 2932)
notify-osd (pid: 3202)
dconf-service (pid: 3210)
eclipse (pid: 10392)
java (pid: 10463)
firefox (pid: 14552)
plugin-containe (pid: 14587)
mate-terminal (pid: 14721)
marco (pid: 19678)
```
