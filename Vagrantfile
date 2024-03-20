# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_BASE = "ubuntu/focal64"
RAM = "512"
CPUS = "2"
SERVER = "server"
CLIENTE = "cliente"

Vagrant.configure("2") do |config|
  config.vm.box = BOX_BASE
  config.vm.define CLIENTE do |cliente|
    cliente.vm.hostname = CLIENTE
    cliente.vm.provider :virtualbox do |vb|
        vb.customize [ 'modifyvm', :id, '--memory', RAM ]
        vb.customize [ 'modifyvm', :id, '--cpus', CPUS ]
        vb.customize [ 'modifyvm', :id, '--name', CLIENTE ]
    end
    cliente.vm.network "private_network", ip: "192.168.56.3"
    cliente.vm.hostname= "cliente"
    cliente.vm.provision "shell", inline: <<-SHELL
        cp /vagrant/cliente.py /home/vagrant/
        sed -i 's/\r$//' /home/vagrant/cliente.py  
    SHELL
    
  end
  config.vm.define SERVER do |server|
    server.vm.hostname = SERVER
    server.vm.provider :virtualbox do |vb|
        vb.customize [ 'modifyvm', :id, '--memory', RAM ]
        vb.customize [ 'modifyvm', :id, '--cpus', CPUS ]
        vb.customize [ 'modifyvm', :id, '--name', SERVER ]
    end
    server.vm.network "private_network", ip: "192.168.56.2"
    server.vm.hostname = "server"
    server.vm.provision "shell", inline: <<-SHELL
    cp /vagrant/server.py /home/vagrant/
        sed -i 's/\r$//' /home/vagrant/server.py
    SHELL
    
  end
end
 