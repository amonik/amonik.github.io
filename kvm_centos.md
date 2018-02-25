# Setup KVM and Install Centos VM with Console Access

```
yum install epel-release
yum update
yum install qemu libvirt libvirt-devel ruby-devel gcc qemu-kvm
yum groupinstall "Development Tools"
yum groupinstall "Virtualization Tools"
yum install virt-install libvirt-python virt-manager virt-install libvirt-client
```
# Setup Image Location
```
mkdir /home/admin/KVM
su - root
semanage fcontext -a -t virt_image_t '/home/admin/KVM(/.*)?'
restorecon /home/admin/KVM
rmdir /var/lib/libvirt/images
ln -s /home/admin/KVM /var/lib/libvirt/images
```
# Create Image File and deploy
```
cd /home/admin/KVM
wget http://mirrors.mit.edu/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1708.iso
qemu-img create -f qcow2 /home/admin/KVM/vm1.qcow2 20G
virt-install --virt-type kvm --vcpu 2 --name vm1 --ram 4096 \
  --disk /home/admin/KVM/vm1.qcow2,format=qcow2   --network network=default \
  --graphics vnc,listen=0.0.0.0 --noautoconsole  \
  --os-type=linux --os-variant=centos7.0 \
  --location=/home/admin/KVM//CentOS-7-x86_64-Minimal-1708.iso
```
Go to your server and go through the installation process.
Log into your serve and get the IP address and SSH.

# Setup Console Access (Run these commands on the vm1)
```
yum install acpid
systemctl enable acpid
echo "NOZEROCONF=yes" >> /etc/sysconfig/network
vi /etc/default/grub
```
* Make the line look like this:
```
GRUB_CMDLINE_LINUX="crashkernel=auto rd.lvm.lv=centos/root rd.lvm.lv=centos/swap console=tty0 console=ttyS0, 115200n8"
```
* Enable the Console Access:
```
grub2-mkconfig -o /boot/grub2/grub.cfg
exit 
```
* Reboot the VM
```
virsh reboot vm1
```
