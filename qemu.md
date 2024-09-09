# QEMU

0. wget https://dl-cdn.alpinelinux.org/alpine/v3.18/releases/x86_64/alpine-standard-3.18.0-x86_64.iso

1. qemu-system-x86_64 -netdev socket,id=vlan0,mcast=230.0.0.1:1234 -object filter-dump,id=dump0,netdev=vlan0,file=log.pcap -net nic,model=e1000,macaddr=56:34:12:00:54:08,id=eth0,netdev=vlan0


--


# VM1
1.  qemu-img create -f qcow2 vm0.qcow2 10G

2.  qemu-system-x86_64 -name vm0 -m 1024 -smp 1 -cdrom alpine-standard-3.18.0-x86_64.iso -drive file=vm0.qcow2,format=qcow2 -netdev socket,id=vlan0,mcast=230.0.0.1:1234 -object filter-dump,id=dump0,netdev=vlan0,file=log0.pcap -net nic,model=e1000,macaddr=56:34:12:00:54:08,netdev=vlan0

3.  /

4.  # basic alpine setup

5.  auto eth0
    iface eth0 inet static
        address 192.168.100.1
        netmask 255.255.255.0

6. /etc/init.d/networking restart

# VM2
1.  qemu-img create -f qcow2 vm1.qcow2 10G

2.  qemu-system-x86_64 -name vm1 -m 1024 -smp 1 -cdrom alpine-standard-3.18.0-x86_64.iso -drive file=vm1.qcow2,format=qcow2 -netdev socket,id=vlan0,mcast=230.0.0.1:1234 -object filter-dump,id=dump0,netdev=vlan0,file=log1.pcap -net nic,model=e1000,macaddr=56:34:12:00:54:09,netdev=vlan0

3.  /etc/network/interfaces

4.  # basic alpine setup

5.  auto eth0
    iface eth0 inet static
        address 192.168.100.2
        netmask 255.255.255.0

6. /etc/init.d/networking restart

# VM3
1.  qemu-img create -f qcow2 vm2.qcow2 10G

2.  qemu-system-x86_64 -name vm2 -m 1024 -smp 1 -cdrom alpine-standard-3.18.0-x86_64.iso -drive file=vm2.qcow2,format=qcow2 -netdev socket,id=vlan0,mcast=230.0.0.1:1234 -object filter-dump,id=dump0,netdev=vlan0,file=log2.pcap -net nic,model=e1000,macaddr=56:34:12:00:54:0A,netdev=vlan0

3.  /etc/network/interfaces

4.  # basic alpine setup

5.  auto eth0
    iface eth0 inet static
        address 192.168.100.3
        netmask 255.255.255.0

6. /etc/init.d/networking restart

# PING
1.  ping 192.168.100.1 # VMX -> VM0
2.  ping 192.168.100.2 # VMX -> VM1
3.  ping 192.168.100.3 # VMX -> VM2
