Vagrant.require_version ">= 1.8.0"

Vagrant.configure(2) do |config|

  # Define Boxes
  config.vm.define "proxy" do |proxy|
    proxy.vm.box = "centos/8"
  end
  config.vm.define "app1" do |app1|
    app1.vm.box = "centos/8"
  end
  config.vm.define "app2" do |app2|
    app2.vm.box = "centos/8"
  end
  config.vm.define "storage" do |storage|
    storage.vm.box = "centos/8"
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
      "proxies" => ["proxy"],
      "proxies:vars" => {"ansible_sudo_pass" => "vagrant"},
      "applications" => ["app1,app2"],
      "applications:vars" => {"ansible_sudo_pass" => "vagrant"},
      "stores" => ["storage"],
      "stores:vars" => {"ansible_sudo_pass" => "vagrant"}      
    }

    # default password for vagrant boxes to allow sudo priviledges
    ansible.extra_vars = {
      ansible_sudo_pass: "vagrant"
    }
  end

end
