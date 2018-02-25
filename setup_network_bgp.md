# Setup virtual switch/router (vyos)

## Install vyos
```
wget https://downloads.vyos.io/release/1.1.8/vyos-1.1.8-amd64.iso

virt-install --virt-type kvm --vcpu 2 --name vyos --ram 2048 \
  --disk /home/admin/KVM/vyos.qcow2,format=qcow2 \
  --network network=default   --graphics vnc,listen=0.0.0.0 \
  --noautoconsole   --os-type=linux --os-variant=centos7.0 \
  --location=/mnt/nfs/home/Servers/Images/VyOS/vyos-1.1.8-amd64.iso
```
## Add an internal interface to vyos

```
virsh attach-interface --domain vyos --type network \
  --source internal1 --model virtio  \       
  --mac 52:54:00:e2:75:cd --config --live
```
## View a network

Each network is attached to a bridge
```
virsh net-dumpxml default
```
```
<network>
  <name>default</name>
  <uuid>dda581c1-9707-40ef-9eb5-9392525d733e</uuid>
  <forward mode='nat'>
    <nat>
      <port start='1024' end='65535'/>
    </nat>
  </forward>
  <bridge name='virbr0' stp='on' delay='0'/>
  <mac address='52:54:00:7c:9a:c3'/>
  <ip address='192.168.122.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.122.2' end='192.168.122.254'/>
    </dhcp>
  </ip>
  <ip family='ipv6' address='fd41:4f6e:a27a:c6f0::1' prefix='64'>
    <dhcp>
      <range start='fd41:4f6e:a27a:c6f0::10' end='fd41:4f6e:a27a:c6f0::ff'/>
    </dhcp>
  </ip>
</network>
```
## Edit a network (like add a new IPv6 address)
```
virsh net-edit default
```
## restart the network
```
virsh destory default
virsh create default
```
As we can see in the above XML the network type is NAT and the bride it is connect to is virbr0

## View the the bridge
```
brctl show
```
## View the IP and bridge configuration of a virtual machine
```
virsh domifaddr vyos
```
```
 Name       MAC address          Protocol     Address
-------------------------------------------------------------------------------
 vnet0      52:54:00:e2:75:cc    ipv6         2001:db8:ca2:2:1::cd/64
 -          -                    ipv4         192.168.122.156/24
 vnet1      52:54:00:e2:75:cd    ipv6         fd00:dcac:faa4:34::16a/64
```
