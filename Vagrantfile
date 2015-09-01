# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# the ip address where the vm can be accessed from the host
vm_ip                   = "172.84.98.33"
host_name               = "dockerbox.sup"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "phusion/ubuntu-14.04-amd64"
  config.vm.box_url = "https://oss-binaries.phusionpassenger.com/vagrant/boxes/latest/ubuntu-14.04-amd64-vbox.box"

  config.vm.network "private_network", ip: vm_ip
  config.vm.hostname = host_name

  config.vm.network "forwarded_port", guest: 2375, host: 2375  # docker
  config.vm.network "forwarded_port", guest: 3800, host: 3800  # sup api
  config.vm.network "forwarded_port", guest: 4300, host: 4300  # sup front end
  config.vm.network "forwarded_port", guest: 36000, host: 36000 # sup livereload

  config.vm.provider "virtualbox" do |v|
    v.name = "superbox"
    v.cpus   = 8
    v.memory = 4096
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

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
end
