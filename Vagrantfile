# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # Basic configuration
  config.vm.box = 'ubuntu/bionic64'

  # Provisioners
  config.vm.provision 'docker' # No params, will simply install Docker for us
  config.vm.provision 'shell', path: 'scripts/install_tools.sh'
  
  # Servers
  1.upto(1) do |i|
    vm_name = "nomad-server#{i}"
    vm_ip = "192.68.50.1#{i}"
    config.vm.define vm_name do |server|
      server.vm.hostname = vm_name
      server.vm.network 'private_network', ip: vm_ip
    end
  end

  # Clients
  1.upto(1) do |i|
    vm_name = "nomad-client#{i}"
    vm_ip = "192.68.60.1#{i}"
    config.vm.define vm_name do |server|
      server.vm.hostname = vm_name
      server.vm.network 'private_network', ip: vm_ip
    end
  end

  # Increase memory for Virtualbox
  config.vm.provider 'virtualbox' do |vb|
    vb.memory = '1024'
  end

  # Increase memory for Parallels Desktop
  config.vm.provider 'parallels' do |p|
    p.memory = '1024'
  end

  # Increase memory for VMware
  %w(vmware_fusion vmware_workstation).each do |p|
    config.vm.provider p do |v|
      v.vmx['memsize'] = '1024'
    end
  end
end
