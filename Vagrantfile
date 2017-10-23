# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "bento/centos-7.4"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  config.vm.define "cephnode2" do |cephnode2|
    cephnode2.vm.network "private_network", ip: "192.168.56.102"
    cephnode2.vm.hostname = "ceph-node2"
    cephnode2.vm.synced_folder ".", "/ceph-ansible"
    cephnode2.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      #vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 4]
      vb.customize ['createhd', '--filename', 'osds/osd4.vdi', '--variant', 'Standard', '--size', 10 * 1024]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', 'osds/osd4.vdi']
      vb.customize ['createhd', '--filename', 'osds/osd5.vdi', '--variant', 'Standard', '--size', 10 * 1024]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', 'osds/osd5.vdi']
      vb.customize ['createhd', '--filename', 'osds/osd6.vdi', '--variant', 'Standard', '--size', 10 * 1024]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 4, '--device', 0, '--type', 'hdd', '--medium', 'osds/osd6.vdi']
    end
  end
  
  config.vm.define "cephnode3" do |cephnode3|
    cephnode3.vm.network "private_network", ip: "192.168.56.103"
    cephnode3.vm.hostname = "ceph-node3"
    cephnode3.vm.synced_folder ".", "/ceph-ansible"
    cephnode3.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      #vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 4]
      vb.customize ['createhd', '--filename', 'osds/osd7.vdi', '--variant', 'Standard', '--size', 10 * 1024]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', 'osds/osd7.vdi']
      vb.customize ['createhd', '--filename', 'osds/osd8.vdi', '--variant', 'Standard', '--size', 10 * 1024]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', 'osds/osd8.vdi']
      vb.customize ['createhd', '--filename', 'osds/osd9.vdi', '--variant', 'Standard', '--size', 10 * 1024]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 4, '--device', 0, '--type', 'hdd', '--medium', 'osds/osd9.vdi']
    end
  end
  
  config.vm.define "cephnode1" do |cephnode1|
    cephnode1.vm.network "private_network", ip: "192.168.56.101"
    cephnode1.vm.hostname = "ceph-node1"
    cephnode1.vm.synced_folder ".", "/ceph-ansible"
    cephnode1.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      #vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 4]
      vb.customize ['createhd', '--filename', 'osds/osd1.vdi', '--variant', 'Standard', '--size', 10 * 1024]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', 'osds/osd1.vdi']
      vb.customize ['createhd', '--filename', 'osds/osd2.vdi', '--variant', 'Standard', '--size', 10 * 1024]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', 'osds/osd2.vdi']
      vb.customize ['createhd', '--filename', 'osds/osd3.vdi', '--variant', 'Standard', '--size', 10 * 1024]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 4, '--device', 0, '--type', 'hdd', '--medium', 'osds/osd3.vdi']
    end
    #cephnode1.vm.provision "ansible" do |ansible|
    #  ansible.playbook = "site.yml"
    #end
    config.vm.provision "shell", inline: <<-SHELL
      yum install ansible -y
      cp /ceph-ansible/ceph-ansible/hosts /etc/ansible/hosts
      ansible-playbook /ceph-ansible/ceph-ansible/site.yml
      yum install s3cmd -y
      install -m 644 -o root -g root /ceph-ansible/confs/s3cmd /root/.s3cmd
      echo Execute o comando abaixo, copie as chaves e altere o arquivo .s3cmd
      echo radosgw-admin user create --uid=marcio --display-name=marcio
    SHELL
  end
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  #config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #  vb.memory = "1024"
  #end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    echo "192.168.56.101 ceph-node1" >> /etc/hosts
    echo "192.168.56.102 ceph-node2" >> /etc/hosts
    echo "192.168.56.103 ceph-node3" >> /etc/hosts
    echo "192.168.56.100 ceph-node" >> /etc/hosts
    mkdir -p /root/.ssh
    install -m 600 -o root -g root /ceph-ansible/chave/authorized_keys /root/.ssh/authorized_keys
    install -m 600 -o root -g root /ceph-ansible/chave/id_rsa /root/.ssh/
    install -m 644 -o root -g root /ceph-ansible/chave/config /root/.ssh/
    yum install haproxy -y
    cp -f /ceph-ansible/confs/haproxy.cfg /etc/haproxy/haproxy.cfg
    systemctl enable haproxy
    systemctl start haproxy
    yum install keepalived -y
    cp -f /ceph-ansible/confs/keepalived.conf /etc/keepalived/keepalived.conf 
    systemctl enable keepalived
    systemctl start keepalived
    yum install vim -y
  SHELL
end
