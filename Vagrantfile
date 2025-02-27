# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Define the base box to use
  config.vm.box = "ubuntu/focal64"

  # Define the master node
  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.56.10"
    master.vm.provision "shell", inline: <<-SHELL
      # Install Docker
      sudo apt-get update
      sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
      sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      sudo apt-get update
      sudo apt-get install -y docker-ce docker-ce-cli containerd.io
      # Initialize Docker Swarm
      sudo docker swarm init --advertise-addr 192.168.56.10
    SHELL
  end

  # Define the worker nodes
  ["node01", "node02", "node03"].each_with_index do |name, index|
    config.vm.define name do |node|
      node.vm.hostname = name
      node.vm.network "private_network", ip: "192.168.56.#{20 + index}"
      node.vm.provision "shell", inline: <<-SHELL
        # Install Docker
        sudo apt-get update
        sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
        sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
        sudo apt-get update
        sudo apt-get install -y docker-ce docker-ce-cli containerd.io
        # Join the Docker Swarm as a worker
        sudo docker swarm join --token $(ssh -o StrictHostKeyChecking=no vagrant@192.168.56.10 "docker swarm join-token -q worker") 192.168.56.10:2377
      SHELL
    end
  end
end
