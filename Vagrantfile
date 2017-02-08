# -*- mode: ruby -*-

Vagrant.configure("2") do |config|
    
    config.vm.define "master-node" do |config|
        config.vm.hostname = "master-node"
        config.vm.network :private_network, ip: "172.16.16.50"
        config.vm.box = "ubuntu/trusty64"

        config.vm.provision "shell", path: "provision/setup.sh"

          # config.vm.provision "shell",
          #   inline: "apt install -y ansible && ansible-galaxy install geerlingguy.elasticsearch"

        config.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "provision/playbook.yaml"
            ansible.groups = {
                'default' => [ "master-node" ]
            }        
            ansible.extra_vars = {
                'esnode' : '172.16.16.50'
            }
        end
    end


    (1..4).each do |i|
        config.vm.define vm_name = "node-%d" % i do |config|
            config.vm.hostname = vm_name
            config.vm.network :private_network, ip: "172.16.16.#{i+100}"
            config.vm.box = "ubuntu/trusty64"

            config.vm.provision "shell", path: "provision/setup.sh"

            config.vm.provision "ansible_local" do |ansible|
                ansible.playbook = "provision/playbook.yaml"
                ansible.groups = {
                    'default' => [ "node-%d" ]
                }
                ansible.extra_vars = {
                    es_node : "node-%d"
                }
            end
            
        end
    end
end