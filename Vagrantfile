# -*- mode: ruby -*-
# vi: set ft=ruby :

# VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|

  config.ssh.insert_key = false
  config.vbguest.auto_update = true

  config.vm.provider :virtualbox do |v|

    # unless Vagrant.has_plugin?("vagrant-vbguest")
    #   puts 'install vagrant-vbguest'
    #   exit -1
    # end

    v.memory = 1024
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.define :docker_host do |guest|
    guest.vm.hostname = "docker.test"
    guest.vm.box = "centos/7"
    guest.vm.network :private_network, ip: "192.168.33.39"
    # guest.vm.synced_folder ".", "/vagrant"
    guest.vm.provision :ansible do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.galaxy_roles_path = 'services/docker/roles'
      ansible.playbook = "services/docker/main.yml"
      # ansible.provisioning_path = "services/docker"
      # ansible.galaxy_role_file = "services/docker/requirements.yml"
      # ansible.pip_args = "-r /vagrant/requirements.txt"
    end

    guest.vm.provider :virtualbox do |v, override|
      v.name = "docker.test"
    end
  end

end
