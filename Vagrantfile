# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
configValues = YAML.load_file("configs/config.yml")
vmData = configValues['vm']

Vagrant::configure("2") do |config|

 config.vm.provider :virtualbox do |vb|
    vb.customize [
      "modifyvm", :id,
      "--memory", "#{vmData['memory']}",
      "--cpus", "#{vmData['cpus']}",
      "--ioapic", "#{vmData['ioapic']}"
      ]
    end

  config.vm.box = "#{vmData['box']}"

  config.vm.hostname = "#{vmData['host_name']}"
  config.vm.synced_folder "#{vmData['synced_folder_from']}", "#{vmData['synced_folder_to']}", type: "#{vmData['synced_folder_type']}"

  config.vm.network :private_network, ip: "#{vmData['network_ip']}"

  config.vm.provision :shell, path: "shell/start.sh"
  config.vm.provision :shell, path: "shell/build-erlang-17.0.sh"

end
