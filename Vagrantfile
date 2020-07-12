Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 2
    vb.customize [ "modifyvm", :id, "--uartmode1", "file", File::NULL ]
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.groups = {
      "gateways" => ["gateway"],
      "offices" => ["office1"],
      "homes" => ["home1"],
#      "homes" => ["home[1:2]"],
#      "group4" => ["other_node-[a:d]"], # silly group definition
#      "all_groups:children" => ["group1", "group2"],
#      "group1:vars" => {"variable1" => 9,
#                        "variable2" => "example"}
    }
  end

  config.vm.define "gateway" do |x|
    x.vm.hostname = "gateway"
    x.vm.network "private_network", ip: "10.200.1.10", nic_type: "virtio"
  end

  config.vm.define "office1" do |x|
    x.vm.hostname = "office1"
    x.vm.network "private_network", ip: "10.200.1.21", nic_type: "virtio"
  end

  config.vm.define "home1" do |x|
    x.vm.hostname = "home1"
    x.vm.network "private_network", ip: "10.200.1.22", nic_type: "virtio"
  end

end
