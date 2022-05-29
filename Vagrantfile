Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.box_check_update = false
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
  end

  config.vm.define "ansible_server" do |ansible_server|
    ansible_server.vm.hostname = "ansible-server"
    ansible_server.vm.synced_folder ".", "/vagrant",  create: true, owner: "vagrant", group: "vagrant"
    ansible_server.vm.network "private_network", ip: "192.168.50.2",
      virtualbox__intnet: true
    ansible_server.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning_playbooks/provisioning_ansible_server.yml"
    end
  end

  config.vm.define "zabbix_server" do |zabbix_server|
    zabbix_server.vm.hostname = "zabbix-server"
    zabbix_server.vm.synced_folder ".", "/vagrant",  create: true, owner: "vagrant", group: "vagrant"
    zabbix_server.vm.network "private_network", ip: "192.168.50.3",
      virtualbox__intnet: true
    zabbix_server.vm.provision :docker
    zabbix_server.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning_playbooks/provisioning_zabbix_server.yml"
    end
  end

  config.vm.define "web_server" do |web_server|
    web_server.vm.hostname = "web-server"
    web_server.vm.synced_folder ".", "/vagrant",  create: true, owner: "vagrant", group: "vagrant"
    web_server.vm.network "private_network", ip: "192.168.50.4",
      virtualbox__intnet: true
    web_server.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning_playbooks/provisioning_web_server.yml"
    end
  end
end