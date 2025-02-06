# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"
  config.vm.network "private_network", ip: "192.168.56.10"
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.provision "shell", name: "general_provisions", inline: <<-SHELL 
    # Updating the vagrant machine
    sudo apt-get -y update
    
    # Installing nodeJS
    sudo apt install nodejs npm -y

  SHELL

  config.vm.provision "shell", name: "app_provisions", inline: <<-SHELL 
    # Creation of the app folder
    sudo mkdir -p /var/www/cluster_machine

    # Setting the permissions 
    sudo chmod 775 -R /var/www/cluster_machine
    sudo chown -R vagrant:www-data /var/www/cluster_machine
    cd /var/www/cluster_machine
    npm install express
    npm install -g loadtest
    # Copying the default.js to the app folder
    sudo cp -vr /vagrant/cluster_files/default.js /var/www/cluster_machine
    sudo cp -vr /vagrant/cluster_files/cluster.js /var/www/cluster_machine
  SHELL
 
end
