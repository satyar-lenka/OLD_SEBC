#### 1. Check vm.swappiness
  
  Before change in all 5 nodes:
  
  ubuntu@ip-172-31-15-56:~$ sudo cat /proc/sys/vm/swappiness
  60

  Changed using below steps
    1. sudo vi /etc/sysctl.conf
    2. Added below line
      vm.swappiness = 1
  
  After change in 5 nodes

  ubuntu@ip-172-31-15-56:~$ sudo cat /proc/sys/vm/swappiness

  1

  ubuntu@ip-172-31-2-47:~$ sudo cat /proc/sys/vm/swappiness

  1

  ubuntu@ip-172-31-13-47:~$ sudo cat /proc/sys/vm/swappiness

  1

  ubuntu@ip-172-31-6-163:~$ sudo cat /proc/sys/vm/swappiness

  1

  ubuntu@ip-172-31-15-252:~$ cat /proc/sys/vm/swappiness

  1

#### 2. Show the mount attributes of your volume(s)


ubuntu@ip-172-31-15-56:~$ df
Filesystem     1K-blocks   Used Available Use% Mounted on
udev             7695476     12   7695464   1% /dev
tmpfs            1540092    340   1539752   1% /run
/dev/xvda1      30822592 825496  28639496   3% /
none                   4      0         4   0% /sys/fs/cgroup
none                5120      0      5120   0% /run/lock
none             7700452      0   7700452   0% /run/shm
none              102400      0    102400   0% /run/user
/dev/xvdb       38565344  49164  36550512   1% /mnt


ubuntu@ip-172-31-2-47:~$ df
Filesystem     1K-blocks   Used Available Use% Mounted on
udev             7695476     12   7695464   1% /dev
tmpfs            1540092    340   1539752   1% /run
/dev/xvda1      30822592 825484  28639508   3% /
none                   4      0         4   0% /sys/fs/cgroup
none                5120      0      5120   0% /run/lock
none             7700452      0   7700452   0% /run/shm
none              102400      0    102400   0% /run/user
/dev/xvdb       38565344  49164  36550512   1% /mnt

ubuntu@ip-172-31-13-47:~$ df
Filesystem     1K-blocks   Used Available Use% Mounted on
udev             7695476     12   7695464   1% /dev
tmpfs            1540092    340   1539752   1% /run
/dev/xvda1      30822592 825476  28639516   3% /
none                   4      0         4   0% /sys/fs/cgroup
none                5120      0      5120   0% /run/lock
none             7700452      0   7700452   0% /run/shm
none              102400      0    102400   0% /run/user
/dev/xvdb       38565344  49164  36550512   1% /mnt

ubuntu@ip-172-31-6-163:~$ df
Filesystem     1K-blocks   Used Available Use% Mounted on
udev             7695476     12   7695464   1% /dev
tmpfs            1540092    340   1539752   1% /run
/dev/xvda1      30822592 825476  28639516   3% /
none                   4      0         4   0% /sys/fs/cgroup
none                5120      0      5120   0% /run/lock
none             7700452      0   7700452   0% /run/shm
none              102400      0    102400   0% /run/user
/dev/xvdb       38565344  49164  36550512   1% /mnt

ubuntu@ip-172-31-15-252:~$ df
Filesystem     1K-blocks   Used Available Use% Mounted on
udev             7695476     12   7695464   1% /dev
tmpfs            1540092    340   1539752   1% /run
/dev/xvda1      30822592 825480  28639512   3% /
none                   4      0         4   0% /sys/fs/cgroup
none                5120      0      5120   0% /run/lock
none             7700452      0   7700452   0% /run/shm
none              102400      0    102400   0% /run/user
/dev/xvdb       38565344  49164  36550512   1% /mnt


#### 4. Disable transparent hugepage support

Before change in all 5 nodes:
ubuntu@ip-172-31-15-56:~$ cat /sys/kernel/mm/transparent_hugepage/enabled
[always] madvise never

changed in 5 nodes
1. installed the sysfsutils package:
    sudo apt install sysfsutils
2. append a line with that setting to /etc/sysfs.conf:
    kernel/mm/transparent_hugepage/enabled = never

After chnage in all 5 nodes

  ubuntu@ip-172-31-15-56:~$ cat /sys/kernel/mm/transparent_hugepage/enabled
  always madvise [never]

  ubuntu@ip-172-31-2-47:~$ cat /sys/kernel/mm/transparent_hugepage/enabled
  always madvise [never]

  ubuntu@ip-172-31-13-47:~$ cat /sys/kernel/mm/transparent_hugepage/enabled
  always madvise [never]

  ubuntu@ip-172-31-6-163:~$ cat /sys/kernel/mm/transparent_hugepage/enabled
  always madvise [never]

  ubuntu@ip-172-31-15-252:~$ cat /sys/kernel/mm/transparent_hugepage/enabled
  always madvise [never]


#### 5.List your network interface configuration
ubuntu@ip-172-31-15-56:~$ ifconfig
eth0      Link encap:Ethernet  HWaddr 0a:89:8f:51:74:89  
          inet addr:172.31.15.56  Bcast:172.31.15.255  Mask:255.255.240.0
          inet6 addr: fe80::889:8fff:fe51:7489/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:320 errors:0 dropped:0 overruns:0 frame:0
          TX packets:310 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:36125 (36.1 KB)  TX bytes:35838 (35.8 KB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

ubuntu@ip-172-31-2-47:~$ ifconfig
eth0      Link encap:Ethernet  HWaddr 0a:f9:90:3c:60:5f  
          inet addr:172.31.2.47  Bcast:172.31.15.255  Mask:255.255.240.0
          inet6 addr: fe80::8f9:90ff:fe3c:605f/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:377 errors:0 dropped:0 overruns:0 frame:0
          TX packets:361 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:41551 (41.5 KB)  TX bytes:42498 (42.4 KB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)


ubuntu@ip-172-31-13-47:~$ ifconfig
eth0      Link encap:Ethernet  HWaddr 0a:af:8d:1f:b5:2b  
          inet addr:172.31.13.47  Bcast:172.31.15.255  Mask:255.255.240.0
          inet6 addr: fe80::8af:8dff:fe1f:b52b/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:395 errors:0 dropped:0 overruns:0 frame:0
          TX packets:361 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:42986 (42.9 KB)  TX bytes:42838 (42.8 KB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
          
          
 ubuntu@ip-172-31-6-163:~$ ifconfig
eth0      Link encap:Ethernet  HWaddr 0a:9b:9b:f6:23:73  
          inet addr:172.31.6.163  Bcast:172.31.15.255  Mask:255.255.240.0
          inet6 addr: fe80::89b:9bff:fef6:2373/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:352 errors:0 dropped:0 overruns:0 frame:0
          TX packets:330 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:39400 (39.4 KB)  TX bytes:42326 (42.3 KB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
          
ubuntu@ip-172-31-15-252:~$ ifconfig
eth0      Link encap:Ethernet  HWaddr 0a:de:96:69:8a:9d  
          inet addr:172.31.15.252  Bcast:172.31.15.255  Mask:255.255.240.0
          inet6 addr: fe80::8de:96ff:fe69:8a9d/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:428 errors:0 dropped:0 overruns:0 frame:0
          TX packets:393 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:47448 (47.4 KB)  TX bytes:49808 (49.8 KB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)


#### 6. Show correct forward and reverse host lookups
ubuntu@ip-172-31-15-56:~$ getent hosts 34.208.40.182
34.208.40.182   ec2-34-208-40-182.us-west-2.compute.amazonaws.com
ubuntu@ip-172-31-15-56:~$ getent hosts hosts 172.31.15.56
172.31.15.56    ip-172-31-15-56.us-west-2.compute.internal

ubuntu@ip-172-31-2-47:~$ getent hosts 34.208.56.131
34.208.56.131   ec2-34-208-56-131.us-west-2.compute.amazonaws.com
ubuntu@ip-172-31-2-47:~$ getent hosts 172.31.2.47
172.31.2.47     ip-172-31-2-47.us-west-2.compute.internal
ubuntu@ip-172-31-2-47:~$ 

ubuntu@ip-172-31-13-47:~$ getent hosts 34.208.54.232
34.208.54.232   ec2-34-208-54-232.us-west-2.compute.amazonaws.com
ubuntu@ip-172-31-13-47:~$ 
ubuntu@ip-172-31-13-47:~$ getent hosts 172.31.13.47
172.31.13.47    ip-172-31-13-47.us-west-2.compute.internal

ubuntu@ip-172-31-6-163:~$ getent hosts 34.208.54.195
34.208.54.195   ec2-34-208-54-195.us-west-2.compute.amazonaws.com
ubuntu@ip-172-31-6-163:~$ 
ubuntu@ip-172-31-6-163:~$ getent hosts 172.31.6.163
172.31.6.163    ip-172-31-6-163.us-west-2.compute.internal
ubuntu@ip-172-31-6-163:~$ 

34.208.1.27     ec2-34-208-1-27.us-west-2.compute.amazonaws.com
ubuntu@ip-172-31-15-252:~$ 
ubuntu@ip-172-31-15-252:~$ getent hosts 172.31.15.252
172.31.15.252   ip-172-31-15-252.us-west-2.compute.internal
ubuntu@ip-172-31-15-252:~$ 

#### 7. Show the nscd service is running

sudo apt-get update
sudo apt-get install nscd
sudo service nscd start

ubuntu@ip-172-31-15-56:~$ sudo service nscd status
 * Status of Name Service Cache Daemon service:                                                                                                                                                              * running.

ubuntu@ip-172-31-2-47:~$ sudo service nscd status
 * Status of Name Service Cache Daemon service:                                                                                                                                                              * running.
 
 ubuntu@ip-172-31-13-47:~$ sudo service nscd status
 * Status of Name Service Cache Daemon service:                                                                                                                                                              * running.

ubuntu@ip-172-31-6-163:~$ sudo service nscd status
 * Status of Name Service Cache Daemon service:                                                                                                                                                              * running.

ubuntu@ip-172-31-15-252:~$ sudo service nscd status
 * Status of Name Service Cache Daemon service:                                                                                                                                                              * running.
#### 8. Show the ntp service is running
sudo apt-get install ntp

ubuntu@ip-172-31-15-56:~$ sudo service ntp status
 * NTP server is running

ubuntu@ip-172-31-2-47:~$ sudo service ntp status
 * NTP server is running

ubuntu@ip-172-31-13-47:~$ sudo service ntp status
 * NTP server is running

ubuntu@ip-172-31-6-163:~$ sudo service ntp status
 * NTP server is running
 
ubuntu@ip-172-31-15-252:~$ sudo service ntp status
 * NTP server is running
