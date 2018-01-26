Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/"
    config.vm.box_version = "1.1.0"

    config.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", 1024]
        v.customize ["modifyvm", :id, "--cpus", 1]
    end

    config.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "playbooks/deploy.yml"
        ansible.inventory_path = "playbooks/hosts"
    end
end
