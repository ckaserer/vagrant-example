#!/bin/ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

#########################
$CPU = 2
$MEMORY = 512
$CPUEXECUTIONCAP = 60
$IP = "192.168.0.2"
$BASEOS = "centos/7"
#########################

Vagrant.configure(2) do |config|
  config.vm.box = $BASEOS

  # Network
  config.vm.network "private_network", ip: $IP

  #CPU / Memory settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = $MEMORY
    vb.cpus = $CPU
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", $CPUEXECUTIONCAP]
  end

  #Provisioning example with docker
  config.vm.provision "docker",
    images: ["centos"] 
end
