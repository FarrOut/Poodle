Vagrant.require_version ">= 1.8.0"

Vagrant.configure(2) do |config|

  # Define Boxes
  config.vm.define "man1" do |man1|
    man1.vm.box = "centos/8"
  end
  config.vm.define "worker1" do |worker1|
    worker1.vm.box = "centos/8"
  end

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "auto"
    ansible.verbose = true

    # Call the default playbook.
    ansible.playbook = "provisioning/site.yml"

    # Optionally filter tags (string or array of strings)
    ansible.tags = ["all"]

    # Set of inventory groups to be included in the auto-generated inventory file.
    ansible.groups = {
      "managers" => ["man1"],
      "managers:vars" => {"ansible_sudo_pass" => "vagrant"},
      "workers" => ["worker1"],
      "workers:vars" => {"ansible_sudo_pass" => "vagrant"}
    }

    # default password for vagrant boxes to allow sudo priviledges
    ansible.extra_vars = {
      ansible_sudo_pass: "vagrant"
    }
  end

end
