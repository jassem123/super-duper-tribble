node_list = [
    { :host => "master-node", :ip=>"192.168.46.10", :cpu => 2 ,:ram => 2028 },
    { :host => "slave-node", :ip=>"192.168.46.11", :cpu => 1 ,:ram => 1024 },
]

varDomain = "dr2p.com"

Vagrant.configure("2") do |config|

    config.vm.synced_folder 'C:/workplace/vagrant/', '/vagrant', type: "virtualbox", disabled: false   
    config.vm.provision "shell", path: "script.sh"
    node_list.each do |node|
        i = 0
        config.vm.define node[:host] do |node_config|
            node_config.vm.box = "centos/7"
            node_config.vm.network "private_network", ip: node[:ip], :netmask => "255.255.255.0"
            node_config.vm.hostname = "#{node[:host]}.#{varDomain}"
            node_config.vm.provider :virtualbox do |v|
                v.name = node[:host].to_s
                v.customize ["modifyvm", :id, "--memory", node[:ram].to_s]
                v.customize ["modifyvm", :id, "--cpus", node[:cpu].to_s]
            end
        end
        i = i + 1 
    end
end