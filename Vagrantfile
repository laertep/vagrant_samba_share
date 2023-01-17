Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.provider "virtualbox" do |vb|
      vb.name = "vm_samba"
      
   end
   config.vm.network "forwarded_port", guest: 80, host: 8080
   config.vm.network "public_network", ip: "172.22.12.80", bridge: "Intel(R) Ethernet Connection I217-LM"
   config.vm.synced_folder "./samba", "/tmp/samba"

   # Procedimento para instalar pacotes no centos/8
   config.vm.provision "shell", path: "script.sh"

   config.vm.provision "shell", inline: <<-SHELL
   sudo cp -Rf /tmp/samba/playbook.yml  /home/vagrant/
   sudo cp -Rf /tmp/samba/servidor /home/vagrant/
   sudo cp -Rf /tmp/samba/roles/ /home/vagrant/
   sudo cp /tmp/samba/ansible.cfg /etc/ansible/
   sudo cp /tmp/samba/smb.conf /etc/samba/
  SHELL
    config.vm.provision "shell", path: "ansible.sh"
end