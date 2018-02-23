Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/trusty64"

    config.vm.define "node1" do |machine|
        machine.vm.network "private_network", ip: "172.17.177.21"
    end

    config.vm.define "node2" do |machine|
        machine.vm.network "private_network", ip: "172.17.177.22"
    end

    config.vm.define 'controller' do |machine|
        machine.vm.network "private_network", ip: "172.17.177.11"
      
        config.vm.provision "file", source: "ansible.cfg", destination: "/home/vagrant/.ansible.cfg"
        config.vm.provision "file", source: "inventory", destination: "/home/vagrant/inventory"
       
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
# vim: set syntax=ruby :
