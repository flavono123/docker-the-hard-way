Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_version = "20220215.1.0"
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "install-docker.yaml"
  end
end
