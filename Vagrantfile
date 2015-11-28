# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "debian/jessie64"
  # Just use the insecure_private_key for convenience
  config.ssh.insert_key = false

  config.vm.define "turnover" do |turnover|
      turnover.vm.hostname = "turnover"
      turnover.vm.network "forwarded_port", guest: 8081, host: 8081
      turnover.vm.provision :shell, path: "bootstrapAnsible.sh"
      turnover.vm.network "public_network", bridge: "wlan0"

      turnover.vm.provider "virtualbox" do |vb|
           # Don't boot with headless mode
           vb.gui = false
           vb.name = "turnoverVM"

           # Use VBoxManage to customize the VM. For example to change memory:
           # vb.customize ["modifyvm", :id, "--memory", "1024"]
      end

      turnover.vm.provision "ansible" do |ansible|
          ansible.playbook = "./ansible/turnover.yml"
      end

      turnover.vm.provision "shell" do |s|
          s.inline = "npm install -g strongloop"
      end

    end


  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

end
