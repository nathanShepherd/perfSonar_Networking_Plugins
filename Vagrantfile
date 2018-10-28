
# Network Infrastructure testing for pScheduler
# Developed by Nathan Shepherd for UofM : ITS

# -*- mode: ruby -*-
# # vi: set ft=ruby :



# Define automated shell script to execute after VM privisioning
$script = <<-SHELL

  # Download, install, and configure a server with pscheduler
  sudo curl -s -O https://raw.githubusercontent.com/perfsonar/pscheduler/master/scripts/system-prep

  sudo sh ./system-prep

  sudo yum install git

  git clone https://github.com/perfsonar/pscheduler.git --branch issue-155
  cd pscheduler
  sudo make

  sudo systemctl stop firewalld

  # Download globus ansible script with git
  sudo yum install ansible
       
  git clone https://github.com/nathanShepherd/Playbook-setup-globus-server.git

SHELL


Vagrant.configure("2") do |config|

  config.vm.define "server" do |server|

    server.vm.box = "geerlingguy/centos7"

    server.vm.network "public_network", ip: "172.28.128.3" #type: "dhcp"

    server.vm.hostname = "server"

    server.vm.provision "shell", inline: $script

  end 

end 
