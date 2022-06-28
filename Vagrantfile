Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_version = "20220215.1.0"

  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
    v.memory = 4096
  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "install-docker.yaml"
  end
end
