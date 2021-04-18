An automation project to help manage my Raspberry Pi Docker Cluster on Ubuntu 20.10 (Groovy Gorilla)

### Install ansible
apt get install ansible

### Modify /etc/hosts to have IPs of Docker Swarm
192.168.0.18 swarm-manager
192.168.0.20 swarm-node1
192.168.0.22 swarm-node2
192.168.0.86 swarm-infra

### Create SSH KeyPair
ssh-keygen

### Copy Public Key To Remote Servers
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@swarm-manager
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@swarm-node1
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@swarm-node2
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@swarm-infra

### Add swarm-infra, [DockerNodes], and [DockerWorkers] to Ansible hosts in /etc/ansible/hosts

swarm-infra

[DockerNodes]
swarm-manager
swarm-node1
swarm-node2

[DockerWorkers]
swarm-node1
swarm-node2


### Run ansible playbook to create swarm
ansible-playbook create_docker_swarm.yml
