# Automate KVM, Network Configuration, Linux, with golang and Python
* Build an API, command line GUI, and make Object Oriented

Installing Ansible:

yum groupinstall "Development Tools"
yum group list
yum install python-virtualenv libffi-devel openssl-devel python-cffi PyYAML
mkdir ansible
cd ansible/
source virenv/bin/activate
virtualenv virenv
source virenv/bin/activate
which python
which pip
pip install upgrade pip
pip install --upgrade pip
pip install ansible
which ansible
ansible --version
pip uninstall ansible
pip install git+https://github.com/ansible/ansible


Test Ansible create a file:

ansible all -m file -a 'path=~/ansible/roles/syslog state=directory mode=755'


Ansible Playbooks, Sections:

All yaml files begin with ‘—‘ and end with three periods ‘…’

Here is list of Playbook keywords that can be included in it:
[playbook Keywords](http://docs.ansible.com/ansible/latest/playbooks_keywords.html)

Run playbook with linux command ‘time’

Often used modules: copy, file

The copy module has a option called content which allow one to directly send a string to a file.

Best practice is to put strings is quotes. Must quote Jinja2 templates. “{{ variable }}”

Handlers, are executed as a notify key from a task that something has changed.

Example:
—
 - name: Some task
   …..
   notify: thing changed

handlers:
   - name: thing changed
     debug:
        msg: The thing changed
…

When Statement:

You can use when statement against various get_facts like the bistro

-name: configure a MOTD
 Copy: 
    Content 
    Dest:
  When: ansible_distribution == “CentOS”

Ansible Playbook Variables:
