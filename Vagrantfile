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

    config.vm.define "nginx" do |config|
        config.vm.hostname = 'nginx'
        config.vm.provision :host_shell do |host_shell|
          host_shell.inline = 'vagrant/bootstrap.sh'
        end

        config.vm.network :private_network, ip: "192.168.100.122"
        config.vm.network :forwarded_port, guest: 22, host: 10102, id: "ssh"
        config.vm.network :forwarded_port, guest: 80, host: 8899, id: "app"
    end

    config.vm.define "jenkins" do |config|
        config.vm.hostname = 'jenkins'

        config.vm.network :private_network, ip: "192.168.100.123"
        config.vm.network :forwarded_port, guest: 22, host: 10101, id: "ssh"
        config.vm.network :forwarded_port, guest: 80, host: 8898, id: "jenkins"
    end
end
