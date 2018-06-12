# -*- mode: ruby -*-
# vi: set ft=ruby :
#
#Vagranfile for Public Network provisioning
#
$device = "br0" #device name for connect to public network
$network = "10.0.1."
$start = 200
$backend_count = 2 #Backend servers quantity
#
Vagrant.configure("2") do |config|
	config.vm.box = "debian/stretch64"
	config.vm.box_version = "9.4.0"
	config.vm.box_check_update = false
	config.vm.provider :libvirt do |libvirt|
 		libvirt.memory = "2048"
		libvirt.cpus = "2"
	end
	(1..$backend_count).each do |i|
		config.vm.define "backend#{i}" do |backendvm| #backend's VMs
 			backendvm.vm.hostname = "ftest-backend#{i}"
			backendvm.vm.network :public_network, ip: $network+"#{$start+i}",
				:dev => $device,
   				:mode => "bridge",
				:type => "bridge"
 		end
	end
	config.vm.define "balancer" do |balancer| #balancer's VM
		balancer.vm.hostname = "ftest-balancer"
		balancer.vm.network :public_network, ip: $network+"#{$start}",
			:dev => $device,
      		:mode => "bridge",
			:type => "bridge"
	end
	config.vm.provision :ansible do |ansible|
		ansible.verbose = "v"    	
		ansible.playbook = "provision.yml"
		ansible.inventory_path = "./hosts"
  	end
end
