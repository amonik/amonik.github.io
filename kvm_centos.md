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
