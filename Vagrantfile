# -*- mode: ruby -*-
# vi: set ft=ruby :

# Variables
node1_box = 'chef/centos-6.5'
node2_box = 'chef/centos-6.5'
node3_box = 'chef/centos-6.5'

Vagrant.configure('2') do |config|
    # node1 configuration
    config.vm.define 'node1' do |node1|
        node1.vm.box = node1_box
        node1.vm.hostname = 'node1.vagrant.local'
        node1.vm.network 'private_network', ip: '192.168.0.10'

        # VM Configuration
        node1.vm.provider :virtualbox do |vbox|
            vbox.customize [
                'modifyvm', :id,
                '--name', 'node1',
                '--memory', '512'
            ]
        end

        # Forwarded Ports
        node1.vm.network 'forwarded_port', guest: 8080, host: 8080

        # hosts configuration
        node1.vm.provision :hosts do |hosts|
            hosts.add_host '192.168.0.20', ['node2.vagrant.local', 'node2']
            hosts.add_host '192.168.0.30', ['node3.vagrant.local', 'node3']
        end
    end

    # node2Configuration
    config.vm.define 'node2' do |node2|
        node2.vm.box = node2_box
        node2.vm.hostname = 'node2.vagrant.local'
        node2.vm.network 'private_network', ip: '192.168.0.20'

        # VM Configuration
        node2.vm.provider :virtualbox do |vbox|
            vbox.customize [
                'modifyvm', :id,
                '--name', 'node2',
                '--memory', '512'
            ]
        end

        # Forwarded Ports
        node2.vm.network 'forwarded_port', guest: 8080, host: 8081

        # hosts configuration
        node2.vm.provision :hosts do |hosts|
            hosts.add_host '192.168.0.10', ['node1.vagrant.local', 'node1']
            hosts.add_host '192.168.0.30', ['node3.vagrant.local', 'node3']
	      end
    end

    config.vm.define 'node3' do |node3|
        node3.vm.box = node3_box
        node3.vm.hostname = 'node3.vagrant.local'
        node3.vm.network 'private_network', ip: '192.168.0.30'

        # VM Configuration
        node3.vm.provider :virtualbox do |vbox|
            vbox.customize [
                'modifyvm', :id,
                '--name', 'node3',
                '--memory', '512'
            ]
        end

        # Forwarded Ports
        node3.vm.network 'forwarded_port', guest: 8080, host: 8082

        # hosts configuration
        node3.vm.provision :hosts do |hosts|
            hosts.add_host '192.168.0.10', ['node1.vagrant.local', 'node1']
            hosts.add_host '192.168.0.20', ['node2.vagrant.local', 'node2']
        end
    end
end
