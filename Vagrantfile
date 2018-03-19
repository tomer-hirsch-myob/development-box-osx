# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

unless Vagrant.has_plugin?("vagrant-cachier")
  puts "Install vagrant-cachier"
  exec 'vagrant plugin install vagrant-cachier && vagrant up'
end

unless Vagrant.has_plugin?("vagrant-vbguest")
  puts "Install vagrant-vbguest"
  exec 'vagrant plugin install vagrant-vbguest && vagrant up'
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "emil-appunite/macos10.13-xcode9.1"

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.hostname = "development-box-osx"

  config.vm.provision "shell", inline: 'su vagrant -c "brew upgrade && brew update"'
  config.vm.provision "shell", inline: 'su vagrant -c "brew doctor || true"'
  config.vm.provision "shell", inline: 'su vagrant -c "brew install python && sudo easy_install pip"'

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
