Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_version = "20220215.1.0"

  config.vm.define 'mgr-1' do |node|
    node.vm.provider "virtualbox" do |v|
      v.name = 'mgr-1'
      v.cpus = 2
      v.memory = 2048
    end

    node.vm.hostname = 'mgr-1'
    node.vm.network :private_network, ip: '192.168.1.2', netmask: '255.255.255.0'
    node.vm.network :forwarded_port, guest: 22, host: 2222, id: 'ssh'
  end

  config.vm.define 'wkr-1' do |node|
    node.vm.provider "virtualbox" do |v|
      v.name = 'wkr-1'
      v.cpus = 2
      v.memory = 2048
    end

    node.vm.hostname = 'wkr-1'
    node.vm.network :private_network, ip: '192.168.1.3', netmask: '255.255.255.0'
    node.vm.network :forwarded_port, guest: 22, host: 2223, id: 'ssh'
  end

  config.vm.define 'wkr-2' do |node|
    node.vm.provider "virtualbox" do |v|
      v.name = 'wkr-2'
      v.cpus = 2
      v.memory = 2048
    end

    node.vm.hostname = 'wkr-2'
    node.vm.network :private_network, ip: '192.168.1.4', netmask: '255.255.255.0'
    node.vm.network :forwarded_port, guest: 22, host: 2224, id: 'ssh'

    node.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "install-docker.yaml"
      ansible.limit = 'all'
    end
  end
end
