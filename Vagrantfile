# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos65"
  config.vm.box_url="https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
  config.vm.hostname = "localhost"
  config.ssh.port = "2222"
  config.ssh.host = "127.0.0.1"
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.synced_folder "./", "/vagrant"

  #mongo
  config.vm.network :forwarded_port, guest: 27017, host: 27017
  config.vm.network :forwarded_port, guest: 27018, host: 27018
  config.vm.network :forwarded_port, guest: 27019, host: 27019
  config.vm.network :forwarded_port, guest: 28017, host: 28017

  #config.vm.provider :virtualbox do |vb|
    #vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  #end

  config.omnibus.chef_version = :latest
  config.berkshelf.enabled = true
  config.berkshelf.berksfile_path = "chef-repo/Berksfile"

  config.vm.provision :chef_solo do |chef|
    chef.json = {
      "tz" => "Japan"
    }
    chef.run_list = [
      "recipe[iptables]",
      "recipe[timezone-ii]",
      "recipe[vim]",
      "recipe[git]",
      "recipe[yum]",
      "recipe[redis2]",
      "recipe[mongodb]"
    ]
  end
end
