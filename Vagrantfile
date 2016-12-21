#!/bin/ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

#########################
$cpus = 4
$memory = 8192
$cpuexecutioncap = 70
$ip = "192.168.0.2"
#########################

#install plugins
  required_plugins = %w(vagrant-hostmanager vagrant-share vagrant-vbguest)
  plugins_to_install = required_plugins.select { |plugin| not Vagrant.has_plugin? plugin }
  if not plugins_to_install.empty?
    puts "Installing plugins: #{plugins_to_install.join(' ')}"
    if system "vagrant plugin install #{plugins_to_install.join(' ')}"
      exec "vagrant #{ARGV.join(' ')}"
    else
      abort "Installation of one or more plugins has failed. Aborting."
    end
  end

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  
  config.vm.network "private_network", ip: $ip

  #CPU / Memory settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = $memory
    vb.cpus = $cpus
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", $cpuexecutioncap]
  end

  #Provisioning example
  config.vm.provision :shell do |shell|
    shell.name = "CentOS Provisioning"
    shell.privileged = "false"
    shell.args = [
      "--verbose",
      "--docker",
    ]
    shell.inline = %{sudo yum install -y git
                   git clone -b master https://github.com/ckaserer/bash-provision.git
                   cd bash-provision
                   git submodule update --init --recursive 
                   exec "/bin/bash" "provision.sh" "$@"}
  end

end