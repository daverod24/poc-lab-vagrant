Vagrant.configure('2') do |config|

    config.vm.box = "bento/centos-7.6"

    config.vm.provider "virtualbox" do |v|

      v.name = "poc-lab"

      v.memory = 1024

      v.cpus = 1

    end

    config.vm.synced_folder ".", "/vagrant", automount: true

    config.vm.network "private_network", ip: "192.168.56.180"

    config.vm.provision "ansible_local" do |ansible|

      ansible.galaxy_roles_path = "/vagrant/roles"

      ansible.playbook = "playbook.yml"
      ansible.verbose = true

    end

  end
