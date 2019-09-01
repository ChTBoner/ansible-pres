# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
servers=[
  {
    :hostname => "centos",
    :ip => "192.168.33.10",
    :box => "centos/7",
    :ram => 512,
    :cpu => 1
  },
  {
    :hostname => "debian",
    :ip => "192.168.33.11",
    :box => "debian/jessie64",
    :ram => 512,
    :cpu => 1
  },
  {
    :hostname => "ubuntu",
    :ip => "192.168.33.12",
    :box => "ubuntu/xenial64",
    :ram => 512,
    :cpu => 1
  },
]

Vagrant.configure(2) do |config|
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network "private_network", ip: machine[:ip]
            node.vm.provider "virtualbox" do |vb|
                vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
            end
        end
    end
  end