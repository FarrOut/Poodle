Vagrant.require_version ">= 1.8.0"

Vagrant.configure(2) do |config|
  config.vm.network :private_network, ip: "192.168.50.4", auto_config: true
  config.vm.usable_port_range = 80..100
  config.vm.hostname = "poodle.local"

  # Define Boxes
  # 'The Boss' is just the manager that is responsible for initiating the Swarm.
  config.vm.define "boss", primary: true do |boss|
    boss.vm.box = "centos/8"
    boss.vm.network "forwarded_port", guest: 80, host: 8080, autocorrect: true
    boss.vm.network "forwarded_port", guest: 443, host: 8443, autocorrect: true
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
      "managers" => ["boss"],
      "swarm" => ["managers"],
      "swarm:vars" => {"ansible_sudo_pass" => "vagrant"}
    }

    # Limit target boxes to a subset.
    ansible.limit = "boss"

    ansible.ask_become_pass = false

    # default password for vagrant boxes to allow sudo priviledges
    ansible.extra_vars = {
      ansible_sudo_pass: "vagrant"
    }
  end

end
