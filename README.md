# Vagrant-Example

**Why no CI?** "Travis does not support running VirtualBox inside any of its compute environments and currently has no plans to support it." (solarce) </br>
Further detail can be found here: [https://github.com/travis-ci/travis-ci/issues/6060]()

---

## Vagrantfile

```ruby
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
  # OS
  config.vm.box = $BASEOS

  # Network
  config.vm.network "private_network", ip: $IP

  # CPU / Memory settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = $MEMORY
    vb.cpus = $CPU
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", $CPUEXECUTIONCAP]
  end

  # Provisioning example with docker
  config.vm.provision "docker",
    images: ["centos"] 
end
```
