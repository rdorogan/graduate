$script = <<SCRIPT
apt-get update >/dev/null
  apt-get install software-properties-common -y
  apt-add-repository ppa:ansible/ansible
  apt-get update >/dev/null
  apt-get install ansible tree mc git zip unzip -y
  chown vagrant:vagrant /home/vagrant/ -R
  echo "SUCCESS"
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.box = "generic/ubuntu1804"
  config.vm.box_check_update = false
  config.vm.synced_folder ".", "/vagrant"
  config.vbguest.no_remote = true
  config.vbguest.auto_update = true

	config.vm.define "controler" do |controler|

	  controler.vm.network "private_network", ip: "192.168.51.51"
	  controler.vm.hostname = "controller"
		
	  controler.vm.provider "virtualbox" do |controller|
		
	    controller.name = "controler"
	    controller.memory = 512
	    controller.cpus = 1
	    controller.gui = false
	
		end
		
	  controler.vm.provision "shell", inline: $script, privileged: true#, run: "always"
		
	end
	
	config.vm.define "jenkins" do |jenkins|

	  jenkins.vm.network "private_network", ip: "192.168.51.52"
	  jenkins.vm.hostname = "Jenkins"
		
	  jenkins.vm.provider "virtualbox" do |jenk|
		
	  jenk.name = "Jenkins"
	  jenk.memory = 1024
	  jenk.cpus = 1
	  jenk.gui = false
	  
	  end
	  end
	  
	config.vm.define "production" do |production|

	  production.vm.network "private_network", ip: "192.168.51.53"
	  production.vm.hostname = "prod"
		
	  production.vm.provider "virtualbox" do |prod|
		
	    prod.name = "prod"
	    prod.memory = 512
	    prod.cpus = 1
	    prod.gui = false
	
	
	end
  end
end