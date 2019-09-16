
# vagrant-multiservers

Example of multiple servers orchestration with Vagrant, Ansible and Puppet


## Prerequisites:

Download and install the following tools:

- [VirtualBox & Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant](https://www.vagrantup.com/downloads.html)

## Running the code

- Status:
  ```bash
  -:$ vagrant status
  ```
- Instantiate the servers:
   ```bash
   -:$ vagrant up server1 server2
   ```
- Verify the instances:
   ```bash
   -:$ vagrant ssh server1 -- "hostname && hostname -I"
   -:$ vagrant ssh server2 -- "hostname && hostname -I"
   ```
- Test communication between servers:
   ```bash
   -:$ vagrant ssh server1 -- "ping -c 4 10.233.89.102"
   -:$ vagrant ssh server2 -- "ping -c 4 10.233.89.101"
   ```

