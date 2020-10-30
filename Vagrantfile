# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # General Vagrant VM configuration.
  config.vm.box = "geerlingguy/centos7"
  config.ssh.insert_key = false
  config.ssh.private_key_path = "~/.ssh/insecure_private_key"
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :virtualbox do |v|
	v.memory = 256
	v.linked_clone = true
  end

 # Wordpress web application
 config.vm.define "app" do |app|
	app.vm.hostname = "wordpress-app.server"
	app.vm.network :private_network, ip: "192.168.60.3"
 end

 # Database server
 config.vm.define "db" do |db|
	db.vm.hostname = "wordpress-db.server"
	db.vm.network :private_network, ip: "192.168.60.4"
 end

 # Config for webserver
 config.vm.provision "ansible" do |ansible|
	ansible.playbook = "webserver.yml"
 end
 
 # Config for database
 config.vm.provision "ansible" do |ansible|
	ansible.playbook = "database.yml"
 end
 
 # Config for WordPress
 config.vm.provision "ansible" do |ansible|
	ansible.playbook = "wordpress.yml"
 end

end
