![GitHub](https://img.shields.io/github/license/ckaserer/vagrant-example)
![Maintenance](https://img.shields.io/maintenance/yes/2019)

<p align="center">
<img width=250px src="https://s3.amazonaws.com/hashicorp-marketing-web-assets/brand/Vagrant_PrimaryLogo_FullColor.HkZvQyRr6g.svg">
</p>

# vagrant-example

The `Vagrantfile` in this repository should help you build your on `Vagrantfile` while learning from the pain that I had to endure figuring out most of it myself.

#### Why no CI?
> Travis does not support running VirtualBox inside any of its compute environments and currently has no plans to support it. ([https://github.com/travis-ci/travis-ci/issues/6060](https://github.com/travis-ci/travis-ci/issues/6060))

## Scenario's covered

### Hungry VM (Virtualbox)
You want to restrict the resources your VM can utilize? And you are working with Virtualbox? Well, then let's take a look how you can restrict memory, cpu and max cpu utilization per core (`cpuexecutioncap`).

```
config.vm.provider "virtualbox" do |vb|
    vb.memory = $MEMORY
    vb.cpus = $CPU
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", $CPUEXECUTIONCAP]
end
```

### ssh not working properly
You are running into issues, when you spin up multiple machines with seperate `Vagrantfile`? Well, that is due to the fact that each VM gets its ssh port forwarded to a port on your host. If two machines try to forward to the same port, things are bound to break. So let's define a port ourselfs.

**Hint:** Keep in mind, that the ssh port needs to be unique on your host system to work.

```
config.vm.network "forwarded_port", guest: 22, host: $SSH, id: 'ssh'
```
  
### static IP

You want to to reach your VM from your hostmachine? Preferably with the same IP every time? Well, then let's define a static IP in your `Vagrantfile`. 

**Hint:** Keep in mind, that the IP needs to be unique on your host system to work.

```
config.vm.network "private_network", ip: $IP
```


