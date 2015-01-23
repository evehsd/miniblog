# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
$init = <<SCRIPT
sudo apt-get -y update
sudo apt-get -y install python-pip
sudo pip install virtualenv
su vagrant -c "virtualenv venv"
/home/vagrant/venv/bin/pip install https://github.com/mitsuhiko/flask/tarball/master
/home/vagrant/venv/bin/pip install pytest
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 1
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end
  
  config.vm.define "miniblog" do |v|
    v.vm.box = "ubuntu1404"
    v.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-i386-vagrant-disk1.box"
    v.vm.hostname = "miniblog"
    v.vm.network "private_network", ip: "192.168.33.70"
    v.ssh.forward_agent = true
    v.vm.provision :shell, :inline => $init
  end
  
end
