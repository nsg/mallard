# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  machines=5

  machines.times do |n|
    config.vm.define "trusty#{n}" do |trusty|
      trusty.vm.hostname = "trusty#{n}"
      trusty.vm.box = "ubuntu/trusty64"
      trusty.ssh.insert_key = false
      trusty.vm.network "public_network", bridge: "eth0"

      if n == machines - 1
        config.vm.provision "ansible" do |ansible|
          ansible.playbook = "setup/site.yml"
          ansible.sudo = true
          ansible.raw_arguments = ["--diff"]
          ansible.limit = 'all'
        end
      end

    end
  end
end
