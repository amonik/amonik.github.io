# Installing Ansible:
```
yum groupinstall "Development Tools"
yum install python-virtualenv libffi-devel openssl-devel python-cffi PyYAML
mkdir ansible
cd ansible/
source virenv/bin/activate
virtualenv virenv
source virenv/bin/activate
pip install --upgrade pip
pip install git+https://github.com/ansible/ansible
```
## Test ping:
ansible all -m ping 



