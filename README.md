
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

## Installing Ansible roles

Execute following command to install required roles for the provided ansible playbook to work:

```bash
  -:$ ansible-galaxy install -r requirements.yml
```

## Running the code

- Status:
  ```bash
  -:$ vagrant status
  ```

### Creating PostgreSQL and PGPool-II servers in separate hosts

- Instantiate PostgreSQL servers:
   ```bash
   -:$ vagrant up --provision postgres01 postgres02
   ```

- Instantiate PGPool-II servers:
   ```bash
   -:$ vagrant up --provision pgpool01 pgpool02
   ```

- Connect to PostgreSQL servers via PGPool-II or directly:
   ```bash
  # Password for "postgres" user is in ./inventories/group_vars/databases.yml file

   -:$ vagrant ssh pgpool01 -- -t "psql -U postgres -p 9999 -h 10.233.89.43"  (1) pgpool01
   -:$ vagrant ssh pgpool01 -- -t "psql -U postgres -p 9999 -h 10.233.89.47"  (2) pgpool02
   -:$ vagrant ssh pgpool01 -- -t "psql -U postgres -p 9999 -h 10.233.89.211" (3) delegate_ip

  # OR

   -:$ vagrant ssh pgpool02 -- -t "psql -U postgres -p 9999 -h 10.233.89.43"  (1) pgpool01
   -:$ vagrant ssh pgpool02 -- -t "psql -U postgres -p 9999 -h 10.233.89.47"  (2) pgpool02
   -:$ vagrant ssh pgpool02 -- -t "psql -U postgres -p 9999 -h 10.233.89.211" (3) delegate_ip

  # OR

   -:$ vagrant ssh postgres01 -- -t "sudo -i -u psql"  (1) postgresql01
   -:$ vagrant ssh postgres02 -- -t "sudo -i -u psql"  (2) postgresql02
   ```

### Creating PostgreSQL and PGPool-II servers in same hosts

- Instantiate servers:
   ```bash
   -:$ vagrant up --provision postgrespool01 postgrespool02
   ```

- Connect via PGPool-II servers' port:
   ```bash
   -:$ vagrant ssh postgrespool01 -- -t "psql -U postgres -p 9999 -h 10.233.89.3"   (1) pgpool in postgrespool01
   -:$ vagrant ssh postgrespool01 -- -t "psql -U postgres -p 9999 -h 10.233.89.5"   (2) pgpool in postgrespool02
   -:$ vagrant ssh postgrespool01 -- -t "psql -U postgres -p 9999 -h 10.233.89.209" (3) pgpool via delegate_ip
   ```
