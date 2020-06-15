Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |v|
    v.name = "nomad"
    v.memory = 2048
    v.cpus = 4
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.hostname = "nomad"
  config.vm.network :private_network, ip: "192.168.100.101"

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "nomad.yml"
    ansible.inventory_path = "testing/inventory"
    ansible.extra_vars = {vaultfile: 'vaults/testing.yml'}
    ansible.limit = "all"
    #ansible.verbose = "vvv"
  end
end
