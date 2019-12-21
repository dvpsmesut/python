IMAGE_NAME = "geerlingguy/ubuntu1604"

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end
      
    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "k8s-master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "kubernetes-setup/master-playbook.yml"
        end
    end

    config.vm.define "node-1" do |node|
        node.vm.box = IMAGE_NAME
        node.vm.network "private_network", ip: "192.168.50.11"
        node.vm.hostname = "node-1"
        node.vm.provision "ansible" do |ansible|
            ansible.playbook = "kubernetes-setup/node-playbook.yml"
        end
    end

    config.vm.define "node-2" do |node|
        node.vm.box = IMAGE_NAME
        node.vm.network "private_network", ip: "192.168.50.12"
        #config.vm.network "forwarded_port", guest: 31514, host: 8000
        node.vm.hostname = "node-2"
        node.vm.provision "ansible" do |ansible|
            ansible.playbook = "kubernetes-setup/node-playbook.yml"
        end
    end

end
