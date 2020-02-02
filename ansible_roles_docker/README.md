# Ansible playbook Docker MySQL master-slave replication

## Those roles doing:

* role docker_ce:

```install docker-ce``
`
```install docker-compose```

```install docker moodule for python```

* role docker_compose:

```- run docker-compose file on managed servers```

```- run connector bash script for mysql replication```

## Pre-requisites:
On your local linux machine:
* Installed [Ansible 2.8.2](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

On managed linux machines:

* Installed Ubuntu Server 18.10 or 18.04

## How to use this roles:

```$ git clone https://github.com/achelak/Ansible-roles.git```

```$ cd Ansible-roles/ansible_roles_docker```

```edit inventory host```

```edit environment variables for mysql master node in ./roles/docker_compose/files/docker-compose.yml```
 
  * Environment variables for master node:

MYSQL_ROOT_PASSWORD: 111
MYSQL_PORT: 3306
MYSQL_USER: mydb_user
MYSQL_PASSWORD: mydb_pwd
MYSQL_DATABASE: mydb
MYSQL_LOWER_CASE_TABLE_NAMES: 0

```edit environment variables for mysql slave node in ./roles/docker_compose/files/docker-compose.yml```

* Environment variables for master node:

MYSQL_ROOT_PASSWORD: 111
MYSQL_PORT: 3306
MYSQL_USER: mydb_slave_user
MYSQL_PASSWORD: mydb_slave_pwd
MYSQL_DATABASE: mydb
MYSQL_LOWER_CASE_TABLE_NAMES: 0

```edit cpu/mem default value in docker-compose file```

* Default cpu/mem value:

cpu_count: 1
cpu_percent: 50
mem_limit: 200m
mem_reservation: 50m

```edit variables in connector bash script ./roles/docker_compose/files/connector.sh```

```$ ansible-playbook docker.yml ```


## After VM's / nodes installation and provisioning:

```check status nodes:```

```$ docker-compose top```

```cheсk mysql slave replication status:```  

```$ docker exec mysql_slave sh -c "export MYSQL_PWD=111; mysql -u root -e 'SHOW SLAVE STATUS \G'"```
~

