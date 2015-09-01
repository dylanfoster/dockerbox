# ![](/assets/vagrant.png) + ![](/assets/docker.png)

dockerbox uses sshfs to share the guest's `code` directory on the host. Any work you plan on doing should be done in this directory

## Installation

**requirements**

 - [ansible](http://docs.ansible.com/ansible/index.html)
 - [ansible-galaxy](https://galaxy.ansible.com/)
 - [vagrant](https://www.vagrantup.com/)

### install vagrant and virtualbox

**Linux**

```shell
$ sudo apt-get install vagrant
$ sudo apt-get install virtualbox
$ sudo apt-get install virtualbox-dkms
```

**OS X**

```shell
$ brew cask install vagrant
$ brew cask install virtualbox
```

### install ansible

**Linux**

```shell
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

**OS X**

```shell
$ brew install ansible
```
### install SSHFS:

**Linux**

```shell
$ sudo apt-get install sshfs
```

**OS X**

```shell
$ brew install Caskroom/cask/osxfuse
$ brew install sshfs
```

### clone the repo:

```shell
$ git clone https://github.com/dylanfoster/dockerbox.git && cd dockerbox
```

### get the requirements:

```shell
$ ansible-galaxy install -r galaxy.yml
```

### start the vm:

```shell
$ vagrant up
```

## License

The MIT License (MIT)

Copyright (c) 2015 Dylan Foster <dylan947@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
