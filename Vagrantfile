# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "ubuntu/trusty64"
    ansible.vm.hostname = "ansible"
    ansible.vm.network "private_network", ip: "192.168.33.10"
    config.ssh.forward_env = ["ansible"]
	ansible.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y python python-pip python-dev build-essential python-setuptools git gcc
    sudo pip install --upgrade pip 
	sudo apt-get install sshpass
    sudo pip install --upgrade virtualenv 
    sudo apt install ansible -y
	ansible.playbook      = "ansible/playbook.yml"
    ansible.sudo          = true

   SHELL
  end
  config.vm.define "docker" do |docker|
    docker.vm.box = "ubuntu/trusty64"
    docker.vm.hostname = "docker"
    docker.vm.network "private_network", ip: "192.168.33.20"
    docker.vm.network "forwarded_port", guest: 80, host:8080 
	docker.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
	sudo apt-get install sshpass
    sudo apt-get install -y python python-pip python-dev build-essential python-setuptools git gcc
    sudo pip install --upgrade pip 
    sudo pip install --upgrade virtualenv 
    sudo apt install ansible -y
    sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo apt-key fingerprint 0EBFCD88
    sudo add-apt-repository \
     "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
     $(lsb_release -cs) \
     stable"
    sudo apt-get update
    sudo apt-get install docker-ce -y
	sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose

   SHELL
  end
  
  
end
