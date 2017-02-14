# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  N = 3
  (1..N).each do |machine_id|
    config.vm.box = "hfm4/centos7"
    #config.vm.box = "centos/7"
    config.vm.define "cassandra-node-#{machine_id}" do |machine|
      machine.vm.hostname = "cassandra-node-#{machine_id}"
      machine.vm.network "private_network", ip: "192.168.5.#{107+machine_id}"
      
      cassandra_vm_memory_mb = 512
      cassandra_port = 9042
      
      cassandra_cluster_info = {
        'cassandra-node-1' => { :node_id => 1 },
        'cassandra-node-2' => { :node_id => 2 },
        'cassandra-node-3' => { :node_id => 3 }
      }
    
      accept_oracle_licence = true
      config.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", "1024"]
        vb.cpus = 1
        if machine_id == N
          machine.vm.provision :ansible do |ansible|
            ansible.limit = "all"
            ansible.playbook = "site.yml"
	    #ansible.groups = {
            # "cassandra" => cassandra_cluster.keys,
           #}
           ansible.verbose = 'vv'
           ansible.sudo = true
           ansible.limit = 'all' # otherwise, Ansible only runs on the current host...
	   ansible.extra_vars = {
             accept_oracle_licence: accept_oracle_licence,
             vagrant_cassandra_cluster_info: cassandra_cluster_info
           }

          end
        end
      end
    end
 end
 config.vm.define "opscenter" do |opscenter|
    opscenter.vm.box = "hfm4/centos7"
    opscenter.vm.network  "private_network", ip: "192.168.5.107"
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "opscenter.yml"
      ansible.verbose = 'vv'
      ansible.sudo = true
      ansible.limit = 'all' 
      config.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", "2048"]
      end
    end
 end
end
