# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'

Vagrant.require_version '>= 1.5.0'

Vagrant.configure('2') do |config|
	config.vm.hostname = 'container'

	if Vagrant.has_plugin?('vagrant-omnibus')
		config.omnibus.chef_version = 'latest'
	end
	
	config.berkshelf.enabled = true
	# config.vm.box = 'chef/ubuntu-14.04'
	config.vm_box = 'opscode-ubuntu-12.04'

	#config.vm.network :private_network, type: 'dhcp'
	config.vm.network :private_network, ip: "192.168.101.101"
	
	# config.vm.provision "docker", images: ["ubuntu"]

	config.vm.provider :virtualbox do |vb, override|
		override.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_ubuntu-12.04_chef-provisionerless.box"
		
		vb.customize ["modifyvm", :id, "--name", "docker-kitchen"]
		vb.customize ["modifyvm", :id, "--memory", "1280"]
		vb.customize ["modifyvm", :id, "--cpus", "2"]
	end
	
	config.vm.provider :vmware_fusion do |vm, override|
		override.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/vmware/opscode_ubuntu-12.04_chef-provisionerless.box"
		
		vm.vmx["memsize"] = "1280"
		vm.vmx["numvcpus"] = "2"
	end

	config.vm.provision 'docker' do |d|
		d.run 'base', image: 'ubuntu:12.04'
	end

#	config.vm.provision :chef_solo do |chef|
#		chef.run_list = ['recipe[docker]']
#		chef.json = {
#		  'docker' => {
#		    'install_type' => 'binary',
#		    'binary' => { 'version' => '0.6.6' },
#		    'bind_socket' => 'unix:///var/run/docker.sock',
#		    'bind_uri' => 'tcp://192.168.101.101:4242'
#		  }
#		}
#	end
end

