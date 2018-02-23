Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/trusty64"

    config.vm.define "mongo" do |machine|
        machine.vm.network "private_network", ip: "172.17.177.10"
        machine.vm.hostname = "mongo"
    end

    config.vm.define "webdev1" do |machine|
        machine.vm.network "private_network", ip: "172.17.177.20"
        machine.vm.hostname = "webdev1"
    end

    config.vm.define "webdev2" do |machine|
        machine.vm.network "private_network", ip: "172.17.177.21"
        machine.vm.hostname = "webdev2"
    end

    config.vm.define 'controller' do |machine|
        machine.vm.network "private_network", ip: "172.17.177.254"
        machine.vm.hostname = "controller"
      
        config.vm.provision "file", source: "ansible.cfg", destination: "/home/vagrant/.ansible.cfg"
        config.vm.provision "file", source: "inventory", destination: "/home/vagrant/inventory"
        config.vm.provision "file", source: "playbook.yml", destination: "/home/vagrant/playbook.yml"
       
        config.vm.synced_folder "./", "/vagrant",
            owner: "vagrant",
            mount_options: ["dmode=775,fmode=600"]

        machine.vm.provision :ansible_local do |ansible|
            ansible.playbook = "playbook.yml"
            ansible.verbose  = true
            ansible.config_file = "ansible.cfg"
            ansible.install = true
            ansible.limit = "all"
            ansible.inventory_path = "inventory"
        end
    end
end
# vim: set syntax=ruby:set ts=4:
