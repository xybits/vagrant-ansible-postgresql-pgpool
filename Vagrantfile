# -*- mode: ruby -*-
# vi: set ft=ruby :

PREFERRED_BOX = 'centos7'
DOMAIN_NAME = 'xybits.vagrant'
BOXES = {
  :centos6    => {
    :box_name => 'centos/6',
    :memory   => 1024,
    :cpus     => 1,
  },
  :centos7    => {
    :box_name => 'centos/7',
    :memory   => 1024,
    :cpus     => 1,
  },
}

INSTANCES  = {
  :server1 => {
    :private_ip => '10.233.89.101',
  },
  :server2 => {
    :private_ip => '10.233.89.102',
  },
}

servers = Hash.new
INSTANCES.each do |server, spec|
  servers["#{server}"] = BOXES[:"#{PREFERRED_BOX}"].merge(spec)
end

Vagrant.configure("2") do |config|
  config.vagrant.plugins     = [ "vagrant-vbguest" ]
  config.vbguest.auto_update = false

  servers.each do |name, machine|
    config.vm.define name, autostart: false do |node|
      full_name = "#{name}".gsub(/_/, "-") + "." + DOMAIN_NAME

      node.vm.box      = machine[:box_name]
      node.vm.hostname = full_name

      # Set Private IP
      if machine[:private_ip] != nil
        node.vm.network "private_network", ip: machine[:private_ip]
      end

      # Provider
      node.vm.provider :virtualbox do |vb|
        vb.name   = full_name
        vb.memory = machine[:memory]
        vb.cpus   = machine[:cpus]
      end
    end
  end
end

