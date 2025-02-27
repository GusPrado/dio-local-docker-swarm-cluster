# Docker Swarm Cluster with Vagrant

This project automates the creation of a local Docker Swarm cluster using Vagrant. It sets up one manager node (`master`) and three worker nodes (`node01`, `node02`, `node03`) with fixed IP addresses and Docker installed.

## Requirements

- **Vagrant**: Install Vagrant from [here](https://www.vagrantup.com/downloads).
- **VirtualBox** (or another Vagrant-supported provider): Install VirtualBox from [here](https://www.virtualbox.org/wiki/Downloads).
- **Git** (optional): To clone this repository.

## How to Use

1. **Clone the Repository** (if applicable):
   ```bash
   git clone <repository-url>
   cd <repository-directory>
```

2. **Start the Cluster**:
Run the following command to create and provision the virtual machines:

```bash
vagrant up
```

3. **Access the Cluster**:

Once the vagrant up command completes, you will have a Docker Swarm cluster running.

You can SSH into any of the virtual machines using:

```bash
vagrant ssh <vm_name>
```
Replace <vm_name> with master, node01, node02, or node03.

4. **Verify the Swarm Cluster**:

- SSH into the master node:

```bash
vagrant ssh master
```

- Run the following command to check the status of the Swarm cluster:

```bash
docker node ls
```

You should see the master node as the manager and the other nodes as workers.

5. **Destroy the Cluster (optional)**:
When you're done, you can destroy the cluster to free up resources:

```bash
vagrant destroy -f
```

## Notes
- **IP Addresses**:
 - master: 192.168.56.10
 - node01: 192.168.56.20
 - node02: 192.168.56.21
 - node03: 192.168.56.22

- **Docker Installation**:
Docker is automatically installed on all nodes during provisioning.

- **Swarm InitializationStart the Cluster**:
Run the following command to create and provision the virtual machines:

- **SSH Access**:
Vagrant automatically configures SSH access to the VMs. Use vagrant ssh <vm_name> to access any node.

- **Resource Allocation**:
By default, Vagrant allocates minimal resources to the VMs. You can customize the VM resources (e.g., CPU, memory) by editing the Vagrantfile.

- **Networking**:
The VMs use a private network with fixed IP addresses. Ensure these IPs do not conflict with your local network.

- **Provider**:
This setup uses VirtualBox by default. If you're using a different provider (e.g., VMware, Hyper-V), make sure to update the Vagrantfile accordingly.
