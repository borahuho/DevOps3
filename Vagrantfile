$useraddscript = <<SCRIPT
useradd -m anna 
groupadd team
groupadd accounting
usermod -aG team anna
mkdir /accounting
SCRIPT


Vagrant.configure('2') do |config|
    config.ssh.insert_key = false

    # set default settings
    config.vm.box = "ubuntu/bionic64"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 1
    end

    config.vm.define :DevOps3, primary: true do |machine|
        machine.vm.host_name = "DevOps3.local"
        machine.vm.network "private_network", ip: "192.168.10.6"
        config.vm.provision "shell", inline: $useraddscript

        machine.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
        end

        machine.vm.synced_folder "DevOps3/", "/home/vagrant/notes"
        machine.vm.provision "file", source: "~/.vagrant.d/insecure_private_key", destination: "$HOME/.ssh/id_rsa"
    end
end


