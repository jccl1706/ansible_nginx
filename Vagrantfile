Vagrant.configure("2") do |config|

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.ssh.insert_key = false
    # my ansible_controller host
  config.vm.define "ansible_controller" do |ansible|
    ansible.vm.box = "bento/ubuntu-20.04"
    #ansible.vm.network "private_network", ip: "192.168.56.101"
    ansible.vm.network "public_network", bridge: "wlo1"
    ansible.vm.hostname = "ansible-controller"
    ansible.vm.provider "virtualbox" do |v|
      v.gui = false
      v.name = "ansible_controller"
      v.memory = 1024
      v.cpus = 2
    end
    # shell provisioner for ansible_controller host
    ansible.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get upgrade -y
      sudo apt-get install -y ansible
      echo "Ansible installed on Ansible Controller"
      sudo apt-get install git -y 
      sudo -u vagrant bash << EOF
      git clone https://github.com/jccl1706/ansible_nginx.git /home/vagrant/ansible_nginx
      cd /home/vagrant/ansible_nginx
EOF
      #chmod +x ./path/to/script/run_this_script.sh
      #./path/to/script/run_this_script.sh
      
    SHELL
  end


  # nginx web1 server 
  config.vm.define "web1" do |web1|
    web1.vm.box = "bento/ubuntu-20.04"
    #web1.vm.network "private_network", ip: "192.168.56.102"
    #web1.vm.network "forwarded_port", guest: 80, host: 8080
    web1.vm.network "public_network", bridge: "wlo1"
    web1.vm.hostname = "web1"
    web1.vm.provider "virtualbox" do |v|
      v.gui = false
      v.name = "web1"
      v.memory = 1024
      v.cpus = 2
    end
  end


  # nginx web2 server 
  config.vm.define "web2" do |web2|
    web2.vm.box = "bento/ubuntu-20.04"
    web2.vm.network "private_network", ip: "192.168.56.103"
    web2.vm.network "forwarded_port", guest: 80, host: 8081
    web2.vm.hostname = "web2"
    web2.vm.provider "virtualbox" do |v|
      v.gui = false
      v.name = "web2"
      v.memory = 1024
      v.cpus = 2
    end
  end
end 
