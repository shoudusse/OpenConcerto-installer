# -*- mode: ruby -*-
# vi: set ft=ruby :

# Adjustable settings
CFG_MEMSIZE = "2048"      # max memory for each VM
CFG_CPUS = "2"
CFG_IP = "192.168.10.2"  # private IP address
CFG_HOSTNAME = "openconcerto"

# VM configurations
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.forward_x11
  config.vm.define :openconcerto do |x|
    x.vm.box = "ubuntu/trusty64"
    x.vm.provider "vmware_fusion" do |v|
      v.vmx["memsize"]  = CFG_MEMSIZE
    end
    x.vm.provider :virtualbox do |v|
      v.name = CFG_HOSTNAME
      v.memory = CFG_MEMSIZE.to_i 
      v.cpus = 2
    end
    x.vm.provider :libvirt do |lv|
      lv.memory = CFG_MEMSIZE.to_i
      lv.cpus = 2
    end
    x.vm.network :private_network, ip: CFG_IP, :libvirt__network_name=> 'vagrant0'
    x.vm.hostname = CFG_HOSTNAME

    x.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/playbook.yml"
      ansible.verbose = "vv"
    end
  end
end
