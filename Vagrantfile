Vagrant.configure("2") do |config|
    config.vm.box = "centos/7"
    config.vm.box_version = v2004.01
    config.vm.box_check_update = false
    config.vm.provider "virtualbox" do |vb|
        vb.gui = false
    end

    config.vm.define "ansible_server" do |ansible_server|
        ansible_server.vm.hostname = "ansible_server"
        ansible_server.vm.synced_folder ".", "/vagrant", disabled: true
        ansible_server.vm.network "private_network", ip: "192.168.1.2"
        ansible_server.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "playbook.yml"
          end
    end
end