# -*- mode: ruby -*-

Vagrant.configure("2") do |config|
    

    # config.vm.define "master-node" do |config|

    #     config.vm.provider "virtualbox" do |vb|
    #         vb.memory = 1000
    #         vb.cpus = 1
    #     end

    #     config.vm.hostname = "master-node"
    #     config.vm.network :private_network, ip: "172.16.16.50"
    #     config.vm.box = "ubuntu/trusty64"

    #     config.vm.provision "ansible_local" do |ansible|
    #         ansible.playbook = "provision/rolesplaybook.yaml"
    #         ansible.groups = {
    #             'default' => [ "master-node" ]
    #         }
    #     end

    #     config.vm.provision "ansible_local" do |ansible|
    #         ansible.playbook = "provision/playbook.yaml"
    #         ansible.groups = {
    #             'default' => [ "master-node" ]
    #         }
    #     end
    # end


    (1..5).each do |i|
        config.vm.define vm_name = "node-%d" % i do |config|

            config.vm.provider "virtualbox" do |vb|
                vb.memory = 12000
                vb.cpus = 3
            end

            config.vm.hostname = vm_name
            config.vm.network :private_network, ip: "172.16.16.#{i+100}"
            config.vm.box = "ubuntu/trusty64"

            config.vm.provision "ansible_local" do |ansible|
                ansible.playbook = "provision/rolesplaybook.yaml"
                ansible.groups = {
                    'default' => [ vm_name ]
                }
            end

            config.vm.provision "ansible_local" do |ansible|
                ansible.playbook = "provision/playbook.yaml"
                ansible.groups = {
                    'default' => [ vm_name ]
                }
            end
            
        end
    end
end