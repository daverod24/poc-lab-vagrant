# -*- mode: ruby -*-
# vi: set ft=ruby :
#configure version values 1 or 2
$VAGRANT_CONFIGURE_VERSION= "2"
##to install a vm with ansible
$regular_node= <<SCRIPT

SCRIPT

#vms array
vms = {
  "poc-labs" => { :box => "bento/centos-7.6",
                  :ip => "192.168.35.3", 
                  :cpus => 1, 
                  :mem => 1500
                  # :disks => [ 8192, 20480, 10240 ] 
                },
  "poc-labs2" => { :box => "bento/centos-7.6",
                  :ip => "192.168.35.4", 
                  :cpus => 1, 
                  :mem => 1500
                  # :disks => [ 8192, 20480, 10240 ] 
                },                
}

Vagrant.configure(2) do |config|
  vms.each_with_index do |(virtualmachine, vminfo), index|
    config.vm.define virtualmachine do |cfg|
      cfg.vm.provider :virtualbox do |vb, override|
        # config.vbguest.auto_update = false
        override.vm.provision "shell", inline: "sed -i '1 s/^/#/' /etc/hosts"
        config.vm.box = vminfo[:box]
        override.vm.network :private_network, ip: vminfo[:ip]
        override.vm.hostname = virtualmachine
        vb.name = virtualmachine
        vb.customize ["modifyvm", :id, "--memory", vminfo[:mem], "--cpus", vminfo[:cpus], "--hwvirtex", "on"]
        # unless vminfo[:disks].nil?
        #   vb.customize ["storagectl", :id, "--name", "SATA", "--add", "sata" ]
        #   vminfo[:disks].each_with_index do |disk, j|
        #     disk_name = "#{Dir.home}/VirtualBox VMs/#{virtualmachine}/disk_#{(j+1).to_s.rjust(2, '0')}.vdi"
        #     unless File.exist?(disk_name)
        #       vb.customize ["createhd", "--filename", disk_name, "--size", disk]
        #     end
        #     vb.customize ["storageattach", :id, "--storagectl", "SATA", "--port", j+1, "--device", 0, "--type", "hdd", "--medium", disk_name]
        #   end
        end
      end # end provider
      # cfg.vm.synced_folder "#{Dir.home}/Downloads/media", "/tmp/media"
    end # end config
  end # end vms
end