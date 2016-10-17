# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "geerlingguy/centos7"
  config.vm.hostname = "blsearch"

  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 8983, host: 8983

  config.vm.synced_folder "blsearch/", "/var/www/blsearch"
  config.vm.synced_folder ".", "/vagrant", disabled: true
  
  #config.vm.network "private_network", ip: "192.168.33.11"

  # config.vm.provider "virtualbox" do |vb|
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end

  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/playbook.yml"
      ansible.sudo = true
      ansible.host_key_checking = false
      # ansible.verbose =  'vvvv'
      ansible.extra_vars = { ansible_ssh_user: 'vagrant', 
          ansible_connection: 'ssh',
          ansible_ssh_args: '-o ForwardAgent=yes'}
  end
end
