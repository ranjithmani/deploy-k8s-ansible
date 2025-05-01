# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure("2") do |config|
  config.vm.synced_folder "src/", "/srv/website", disabled: true
  config.vm.synced_folder ".", "/vagrant", disabled: true

end
MASTER_IP       = "master-ip"
NODE_01_IP      = "worker-ip"
NODE_02_IP      = "worker-ip"

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-24.04"
  config.vm.box_version = "202404.26.0"

  boxes = [
    { :name => "master",  :ip => MASTER_IP,  :cpus => 2, :memory => 2048 },
    { :name => "worker1", :ip => NODE_01_IP, :cpus => 1, :memory => 1048 },
    { :name => "worker2", :ip => NODE_02_IP, :cpus => 1, :memory => 1048 },
  ]

  boxes.each do |opts|
    config.vm.define opts[:name] do |box|
      box.vm.hostname = opts[:name]
      box.vm.network :private_network, ip: opts[:ip]
 
      box.vm.provider "libvirt" do |vb|
        vb.cpus = opts[:cpus]
        vb.memory = opts[:memory]
      end
      box.vm.provision "shell", path:"./common.sh"
 

    end
  end
end
