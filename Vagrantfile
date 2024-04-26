Vagrant.configure("2") do |config|
    config.vm.box = "generic/centos8s"
    #config.vm.box_version = "2004.01"
 
    config.vm.provider :virtualbox do |v|
      v.memory = 2048
      v.cpus = 2
    end
  
    # Указываем имена хостов и их IP-адреса
    boxes = [
      { :name => "node1",
        :ip => "192.168.57.11",
      },
      { :name => "node2",
        :ip => "192.168.57.12",
      },
      { :name => "barman",
        :ip => "192.168.57.13",
      }
    ]
    # Цикл запуска виртуальных машин
    boxes.each do |psql|
      config.vm.define psql[:name] do |config|
        config.vm.hostname = psql[:name]
        config.vm.network "private_network", ip: psql[:ip]
        if psql[:name] == "barman"
        config.vm.provision "ansible" do |ansible|
      #ansible.verbose = "vvv"
      ansible.limit = "all"
      ansible.playbook = "ansible/provision.yml"
      ansible.host_key_checking = "false"
      ansible.compatibility_mode = "2.0"
      ansible.become = "true"
      ansible.inventory_path = "ansible/hosts"
     end
    end
  end
end
end
