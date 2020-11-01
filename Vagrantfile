# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
 
 # Provision webserver
 if Vagrant::Util::Platform.windows?
   config.vm.provision :guest_ansible do |ansible|
   ansible.playbook = "playbook.yml"
  end
 else
   config.vm.provision :ansible do |ansible|
   ansible.playbook = "playbook.yml"
  end
 end

 # Generate VM config
 config.vm.box = "geerlingguy/centos7"
 config.ssh.insert_key = false
 config.ssh.private_key_path = "~/.ssh/insecure_private_key"
 config.vm.synced_folder ".", "/vagrant", disabled: true
 config.vm.provider :virtualbox do |vb|
	vb.memory = 512
	vb.linked_clone = true
 end

 # Wordpresserver
 config.vm.define "application" do |app|
 	app.vm.hostname = "wordpress-server"
 	app.vm.network :private_network, ip: "192.168.60.2"
 end

 # Database server
 config.vm.define "database" do |db|
	db.vm.hostname = "wordpress-database"
	db.vm.network :private_network, ip: "192.168.60.3"
 end
end
