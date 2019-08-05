# -*- mode: ruby -*-
# vi: set ft=ruby :
#configure version values 1 or 2
$VAGRANT_CONFIGURE_VERSION= '2'
##to install a vm with ansible
$regular_node= <<SCRIPT

SCRIPT

#vms array
vms = {
  "poc-labs" => { :box => "bento/centos-7.6", :ip => "192.168.35.5", :cpus => 1, :mem => 1500 },
#  "poc-labs2-ubuntu" => { :box => "bento/ubuntu-18.04", :ip => "192.168.35.6", :cpus => 1, :mem => 1500 },
}

Vagrant.configure(2) do |config|
    vms.each_with_index do |(virtualmachine, vminfo), index|
      config.vm.define virtualmachine do |cfg|
        cfg.vm.provider :virtualbox do |vb, override|
          config.vbguest.auto_update = false
#          override.vm.provision "shell", inline: "sed -i '1 s/^/#/' /etc/hosts; echo -e '\n192.168.35.5\tpoc-labs\n192.168.35.6\tpoc-labs2\n192.168.35.7\tpoc-labs3' >> /etc/hosts; mkdir /u01"
          config.vm.box = vminfo[:box]
          override.vm.network :private_network, ip: vminfo[:ip]
#          config.vm.network "forwarded_port", guest: 80, host: 8086
          override.vm.hostname = virtualmachine
          vb.name = virtualmachine
          vb.customize ["modifyvm", :id, "--memory", vminfo[:mem], "--cpus", vminfo[:cpus], "--hwvirtex", "on"]
        end # end provider
        # cfg.vm.synced_folder "/home/user/media", "/tmp/media"
      end # end config
      config.vm.provision "ansible_local" do |ansible|

#        ansible.inventory_path = "/vagrant/inventory"
        ansible.galaxy_roles_path = "/vagrant/provision/roles"        
        ansible.galaxy_role_file = "requirements.yml"
#        ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
        ansible.galaxy_command = "sudo ansible-galaxy install -r requirements.yml -p ./provision/roles"        
        ansible.playbook = "provision/playbook.yml"
#        ansible.verbose = true
        ansible.verbose = "vv"
  
      end # end provision ansible 
    end # end vms
  end