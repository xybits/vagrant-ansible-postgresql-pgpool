
# vagrant-ansible-postgresql-pgpool

Example of [PostgreSQL](https://www.postgresql.org/docs/11/high-availability.html) cluster
with [PGPool-II](https://www.pgpool.net/docs/41/en/html/example-cluster.html)

## Limitation
This example assumes you are familiar with the PostgreSQL replication and PGPool-II high availability concepts.
This example uses two PostgreSQL servers: one master and one standby.

## Prerequisites:

Download and install the following tools:

- [VirtualBox & Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant](https://www.vagrantup.com/downloads.html)
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) 2.8+

## Running the code

- Status:
  ```bash
  -:$ vagrant status
  ```
- Instantiate servers:
   ```bash
   -:$ vagrant up postgresql01 postgresql02
   ```

- Connect to the master server via PGPool-II port
   ```bash
   -:$ vagrant ssh postgresql01 -- -t "sudo -i -u postgres psql -p 9999"
   ```

