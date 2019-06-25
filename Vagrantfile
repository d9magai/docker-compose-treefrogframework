$script = <<SCRIPT
set -eux
curl -fsSL https://get.docker.com/ | sudo sh
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo gpasswd -a $USER docker
sudo systemctl restart docker
sudo systemctl enable docker
SCRIPT

# -*- coding: utf-8 -*-
VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vbguest.auto_update = true
  config.vm.box = "bento/centos-7.6"
  config.vm.network :private_network, ip: "192.168.99.199"
  config.vm.provision "shell", privileged: false, inline: $script
  config.vm.synced_folder ".", "/home/vagrant/workdir", :mount_options => ['dmode=744', 'fmode=644']
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024", "--cpus", "2", "--ioapic", "on", "--audio", "none"]
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/home/vagrant/workdir","1"]
  end
end

