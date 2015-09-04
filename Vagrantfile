# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# the ip address where the vm can be accessed from the host
vm_ip                   = "192.168.99.10"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: vm_ip

  config.vm.network "forwarded_port", guest: 2375, host: 2375  # docker

  config.vm.provider "virtualbox" do |v|
    v.name = "superbox"
    v.cpus   = 8
    v.memory = 4096
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.provision :shell, inline: <<-EOF
    sudo chown -R vagrant /usr/local
  EOF

  config.vm.provision "ansible" do |ansible|
    ansible.sudo = true
    ansible.playbook = "playbook.yml"
  end

  config.vm.provision :shell, run: 'always', inline: <<-EOF
    mkdir -p /home/vagrant/code
  EOF

  config.vm.provision :host_shell, run: 'always' do |hs|
    hs.inline = <<-EOF
      VAGRANT_SSH_CONFIG=~/.ssh/vagrant-config
      vagrant ssh-config --host=vagrant > "$VAGRANT_SSH_CONFIG"

      SSHFS_OPTS="-o reconnect -o allow_other -o sshfs_sync"

      [ ! -d code ] || diskutil unmount force code
      [ -d code ] || mkdir code
      sshfs -F "$VAGRANT_SSH_CONFIG" -p 2222 $SSHFS_OPTS vagrant:/home/vagrant/code code
    EOF
  end

  config.vm.provision :shell, inline: <<-EOF
    sudo chown -R vagrant /home/vagrant/code
  EOF
end

# load extra Vagrantfile which can be used to specify user specific configurations
begin
  load 'VagrantFile.user'
rescue LoadError
  # ignore
end
