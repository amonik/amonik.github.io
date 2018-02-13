# Setup Syslog Using Ansible

* Clone and run the following Ansible scripts

* Test syslog 
  - From a system that has access to your syslog server run this command:
  ```
  logger --tcp --server syslog --port 10514 "Testing Syslog Server"
  ```

