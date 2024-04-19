# -*- mode: ruby -*-
# vi: set ft=ruby  :

servers = {
    "server1" => {"image" => "bento/ubuntu-22.04", "memory" => "1024", "cpu" => "2"},
    "server2" => {"image" => "bento/centos-7.2", "memory" => "1024", "cpu" => "2"}
}

Vagrant.configure("2") do |config|
    servers.each do |name, conf|
        config.vm.define "#{name}" do |machine|
            machine.vm.box_check_update = false
            machine.vm.boot_timeout = 1440
            machine.vm.box = "#{conf["image"]}"
            machine.vm.network "public_network"
            machine.vm.provider "virtualbox" do |vb|
                vb.name = "#{name}"
                vb.memory = conf["memory"]
                vb.cpus = conf["cpu"]
            end
            if "#{name}" == "server1"
                machine.vm.provision "shell", inline: "apt-get update && apt-get install -y apache2"
            else
                machine.vm.provision "shell", inline: "yum install -y httpd"
            end
        end
    end
end
