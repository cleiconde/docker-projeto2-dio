# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
  "diomaster" => {"memory" => "1024", "cpu" => "2", "ip" => "100", "image" => "ubuntu/bionic64"},
  "dionode01" => {"memory" => "1024", "cpu" => "2", "ip" => "101", "image" => "ubuntu/bionic64"},
  "dionode02" => {"memory" => "1024", "cpu" => "2", "ip" => "102", "image" => "ubuntu/bionic64"},
  "dionode03" => {"memory" => "1024", "cpu" => "2", "ip" => "103", "image" => "ubuntu/bionic64"}
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "192.168.56.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.customize ["modifyvm", :id, "--groups", "/DIO-Docker-Lab"]
      end
      machine.vm.provision "shell", path: "docker.sh"
      if "#{name}" == "diomaster"
        machine.vm.provision "shell", path: "master.sh"
      else
        machine.vm.provision "shell", path: "worker.sh"
      end
    end
  end
end
