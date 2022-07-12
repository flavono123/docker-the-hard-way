Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_version = "20220215.1.0"

  config.vm.define 'node1' do |node|
    node.vm.provider "virtualbox" do |v|
      v.name = 'node1'
      v.cpus = 2
      v.memory = 2048
    end

    node.vm.hostname = 'node1'
    node.vm.network :private_network, ip: '192.168.1.2', netmask: '255.255.255.0'
    node.vm.network :private_network, ip: '10.244.1.3', netmask: '255.255.255.240'
    node.vm.network :forwarded_port, guest: 22, host: 2222, id: 'ssh'
  end

  config.vm.define 'node2' do |node|
    node.vm.provider "virtualbox" do |v|
      v.name = 'node2'
      v.cpus = 2
      v.memory = 2048
    end

    node.vm.hostname = 'node2'
    node.vm.network :private_network, ip: '172.31.1.2', netmask: '255.255.255.0'
    node.vm.network :private_network, ip: '10.244.1.4', netmask: '255.255.255.240'
    node.vm.network :forwarded_port, guest: 22, host: 2223, id: 'ssh'

    node.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "install-docker.yaml"
      ansible.limit = 'all'
    end
  end

  config.vm.define 'router' do |router|
    router.vm.provider "virtualbox" do |v|
      v.name = 'router'
      v.cpus = 2
      v.memory = 1024
    end

    router.vm.hostname = 'router'
    router.vm.network :private_network, ip: '10.244.1.2', netmask: '255.255.255.240'
    router.vm.network :private_network, ip: '192.168.1.3', netmask: '255.255.255.0'
    router.vm.network :private_network, ip: '172.31.1.3', netmask: '255.255.255.0'
    router.vm.network :forwarded_port, guest: 22, host: 2224, id: 'ssh'
  end
end
