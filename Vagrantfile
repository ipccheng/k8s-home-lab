# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  (1..3).each do |i|
    config.vm.define "vhomek8sworker#{i}" do |node|
      node.vm.hostname = "vhomek8sworker#{i}"

      node.vm.network "public_network", ip: "192.168.1.11#{i}", bridge: "eno1"

      node.vm.provider "virtualbox" do |vb|
        vb.name = "vhomek8sworker#{i}" 
        vb.cpus = 2
        vb.memory = "2048"
      end

      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "/home/administrator/Projects/k8s/worker-playbook.yml"
        ansible.extra_vars = {
          node_ip: "192.168.1.11#{i}",
        }
      end
    end
  end
end