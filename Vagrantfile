Vagrant.configure("2") do |config| 

    config.vm.box = "bento/ubuntu-16.04"

    config.vm.box_check_update = false

    config.vm.provider "virtualbox" do |vb|
        
        #vb.gui = true
        vb.memory = "1024"
        vb.cpus = 2
        vb.customize ["modifyvm",:id,"--vram","16"]
    end

    config.vm.network "forwarded_port", guest: 80, host:8080, host_ip:  "127.0.0.1"

    config.vm.network "private_network", type: "dhcp"

    config.vm.synced_folder "./public_data" , "/var/www/html"



    $script = <<-SCRIPT
    apt-get -y update
    apt-get install -y nginx
    SCRIPT

    config.vm.provision "shell", inline: $script
    config.vm.provision "shell", path: "provisioner/services.sh"
    config.vm.provision "file", source: "files/login.html",destination: "/var/www/html/login.html"


end