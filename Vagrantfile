NAGENT = 2

Vagrant.configure(2) do |config|


  (1..NAGENT).each do |i|
    config.vm.define "agent-#{i}" do |node|
      node.vm.box = 'centos/7'
      node.vm.hostname = "agent-#{i}"

      # BRIDGE
      node.vm.network 'private_network', ip: "192.168.0.#{i + 9}"

      # Expose web
      config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true

      node.vm.provider :vertualbox do |v|
        v.cpus = 1
        v.memory = 1024
      end

      # provision only when all nodes started
      if i == NAGENT
        node.vm.provision 'ansible' do |ansible|
          ansible.limit = "all"
          ansible.playbook = 'ansible/bootstrap.yml'
        end
      end
    end
  end

end
