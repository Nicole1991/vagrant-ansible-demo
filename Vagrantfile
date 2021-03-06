Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 1024]
        v.customize ["modifyvm", :id, "--cpus", 1]
    end

    config.vm.provision :ansible do |ansible|
        ansible.verbose = "vv"
        ansible.playbook = "playbooks/deploy.yml"
        ansible.inventory_path = "playbooks/hosts"
    end

    config.vm.define "nginx" do |config|
        config.vm.hostname = 'nginx'
        config.vm.provision :host_shell do |host_shell|
            host_shell.inline = 'vagrant/bootstrap.sh'
        end

        config.vm.network :private_network, ip: "192.168.100.122"
        config.vm.network :forwarded_port, guest: 22, host: 10000, id: "ssh"
        config.vm.network :forwarded_port, guest: 80, host: 8899, id: "app"
    end

    config.vm.define "jenkins" do |config|
        config.vm.hostname = 'jenkins'

        config.vm.network :private_network, ip: "192.168.100.123"
        config.vm.network :forwarded_port, guest: 22, host: 10001, id: "ssh"
        config.vm.network :forwarded_port, guest: 8080, host: 8877, id: "jenkins"
    end
end
