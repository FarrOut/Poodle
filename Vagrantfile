Vagrant.require_version ">= 1.8.0"

Vagrant.configure(2) do |config|
  config.vm.network :private_network, ip: "192.168.50.4", auto_config: true
  config.vm.usable_port_range = 8080..8999
  config.vm.hostname = "poodle.local"

  # Define Boxes
  config.vm.define "manager", primary: true do |manager|
    manager.vm.box = "centos/8"
    manager.vm.network "forwarded_port", guest: 8080, host: 8080, autocorrect: true
  end

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "auto"
    ansible.verbose = "vv"

    # Call the default playbook.
    ansible.playbook = "provisioning/site.yml"

    # Optionally filter tags (string or array of strings)
    ansible.tags = ["all"]

    # Set of inventory groups to be included in the auto-generated inventory file.
    ansible.groups = {
      "managers" => ["manager"],
      "swarm" => ["managers"],
      "swarm:vars" => {"ansible_sudo_pass" => "vagrant"}
    }

    ansible.limit = "managers"

    # default password for vagrant boxes to allow sudo priviledges
    ansible.extra_vars = {
      ansible_sudo_pass: "vagrant"
    }
  end

end
