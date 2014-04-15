# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  HOSTS = [
    ["v-wordpress01", 20],
  ]

  HOSTS.each do |(hostname, last_octet)|
    ip = "192.168.203." + last_octet.to_s
    config.vm.define hostname do |cfg|
      cfg.vm.hostname = hostname
      cfg.vm.box = "centos-64-x64-fusion-nocm"
      cfg.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-64-x64-fusion503-nocm.box"
      cfg.vm.network :private_network, ip: ip
      cfg.vm.synced_folder "/opt", "/src"

      # Apply virtualbox-specific overrides.
      cfg.vm.provider "virtualbox" do |v, override|
        override.vm.box = "centos-65-x64-vbox-nocm"
        override.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-65-x64-virtualbox-nocm.box"
      end
#      cfg.vm.provision :ansible do |ansible|
#        ansible.playbook = "site.yml"
#        ansible.host_key_checking = "false"
#        ansible.verbose = "v"
#        ansible.extra_vars = {
#          env: "vagrant",
#          vagrant: "true"
#        }
#      end
    end
  end
end

