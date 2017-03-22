      sysctl vm.swappiness=1
      echo never > /sys/kernel/mm/transparent_hugepage/enabled
     echo never > /sys/kernel/mm/transparent_hugepage/defrag
     sudo chmod +x /etc/rc.d/rc.local
      netstat -i
      cat /etc/hosts
      hostname
      nslookup ip-172-31-2-52.us-west-2.compute.internal 
      yum install bind-utils
     nslookup ip-172-31-2-52.us-west-2.compute.internal 
     nslookup 172.31.2.52
    yum install nscd
     service nscd start
     service nscd status
     yum install ntp ntpdate ntp-doc
     service ntpd start
     service ntpd status
