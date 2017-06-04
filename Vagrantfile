# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # директория запуска вагранта монтируется в /app
  # для удобства разработки
  config.vm.synced_folder '.', '/app'

  config.vm.define 'test-vm' do |app|
    app.vm.box = 'x230/centos7'
    app.vm.box_version = '0.1.0'
    app.vm.box_check_update = false
    app.vm.hostname = 'test-vm'
    app.vm.network 'private_network', ip: '10.100.1.11'
    app.vm.provider 'virtualbox' do |vbox|
      vbox.customize ['setextradata', :id, 'VBoxInternal2/SharedFoldersEnableSymlinksCreate//app', '1']
      vbox.memory = 2048
      vbox.cpus = 2
    end
  end

  config.vm.provision "shell", inline: <<-SHELL
    gem install dapp
    usermod -aG docker vagrant
  SHELL
end
