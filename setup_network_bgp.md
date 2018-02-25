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
