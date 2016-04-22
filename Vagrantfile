#If this box is not on your machine, vagrant up base and make that a base box. Then add that to vagrant
$ubuntu_box = "ubuntu/trusty64"
$num_instances = 3

def medium(config)
    config.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
    end
end

def large(config)
    config.vm.provider "virtualbox" do |v|
      v.memory = 2048 
      v.cpus = 2
    end
end

Vagrant.configure(2) do |config|
    (1..$num_instances).each do |i|
        config.vm.define "node-#{i}" do |build_boot|
            medium(config)
            build_boot.vm.box = $ubuntu_box
            build_boot.vm.hostname = "node-#{i}"
            build_boot.vm.network "private_network", ip: "10.10.10.1#{i}", virtualbox__intnet: "prov"
            build_boot.vm.provision :shell, path: "ssh.sh", privileged: false
            #build_boot.vm.provision :shell, path: "provision_scripts/packages.sh"
            #build_boot.vm.provision :shell, path: "provision_scripts/build.sh", privileged: false
            #build_boot.vm.provision :shell, path: "provision_scripts/cluster-prep.sh", privileged: false
            #build_boot.vm.provision :shell, path: "provision_scripts/dnsmasq.sh"
        end
    end
end
