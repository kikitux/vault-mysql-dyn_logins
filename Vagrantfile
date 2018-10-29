Vagrant.configure("2") do |config|
  
  config.vm.define "vault" do |vault|
    config.vm.box = "alvaro/xenial64"

    # set VM specs
    config.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
    end

    config.vm.provision :shell, :path => "scripts/provision.sh"
    config.vm.provision :shell, :path => "scripts/vault.sh", run: "always"

    config.vm.define "node01" do |l1|
      l1.vm.hostname = "node01"
      l1.vm.network "private_network", ip: "192.168.2.10"
      l1.vm.network "forwarded_port", guest: 8200, host: 8200
    end
  end
  
  config.vm.define "db" do |db|
    db.vm.box = "achuchulev/centos7_mysql"
    
    # set VM specs
    config.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
    end

    config.vm.define "mysql01" do |l1|
      l1.vm.hostname = "mysql01"
      l1.vm.network "private_network", ip: "192.168.2.20"
      l1.vm.network "forwarded_port", guest: 3306, host: 3306
    end
  end

end