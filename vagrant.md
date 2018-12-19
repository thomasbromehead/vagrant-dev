# Vagrant Course

## Commands
1. ___```vagrant status```____ : lets you see the status of the only VM running
2. ___```vagrant global-status```___ : lets you see the state of the VMs
3. ___```vagrant halt ID```___ :
4. ___```vagrant halt```___ :
5. ___```vagrant global-status```___ : Will delete all resources associated with the box but will leave Vagrantfile intact.

## Vagrant runs in headless mode by default

### Common method to connect remotely to Linux operating system is SSH. Vagrant includes an SSH client.

> type exit to log out of the box.

Bases boxes that you customize.

##  Vagrant Cloud
Browse by name or provider
ex: bento => all boxes from bento corp.
Ability to share boxes is the key feature.

## Vagrantfile
Simple Ruby programs to set attributes (CPU, disk, memory, network config)

> Vagrant.configure("2") do |config|
2 refers to the version we are using.

> config.vm.box = "base"
indicates name of box we are using

> config.vm.box = "bento/ubuntu-16.04"

> config.vm.box_check_update = false
Checks for updates to the box on bootup

> config.vm.network "forwarded_port", guest: 80, host: 8080

.config.vm.synced_folder "../data", "/vagrant_data"
Allows you to create a synced folder between VM and local

vagrant folder is automatically created at /vagrant of the box

```vagrant reload``` does a ```vagrant halt``` and a ```vagrant up```

# Vagrant networking
Vagrant boxes are insecure by default, with no name and password
## Port forwarding
1. FTP: 21
2. HTTP 80
3. HTTPS/TLS 443

___**Port Mapping**___ :
To install nginx: sudo apt-get install -y nginx

To create a private, non-routable network address:
config.vm.network "private_network", type: "dhcp"

Retrieve address using: ifconfig
172.28.128.3 --> 172 is private

## Vagrant includes support for building Docker containers

You can run your or settings OR run provider settings

To see details of the VM run
```vmstat -s```

```lscpu``` to see how many CPUs are allocated to it.

VM Provider = Virtualbox or Hyper-V 

Configuration is done in this Ruby block:
``` 
config.vm.provider "virtualbox" do |vb|
 # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
    vb.memory = "512"
    vb.cpus = 2
  end
  ```

  We've been running the box in headless mode, without GUI.

  ```lspci -v -s 00:02.0``` opens up config for GUI

  ```vb.customize ["modifyvm", :id, "--vram", "16"]```
  uses a VBox utility called VBoxManage

### Every base box supports at least 1 and often to several providers. Be aware that if you have a different superviser, you'll have to use --provider when using vagrant up.

Vagrant provisioners are scripts that can be defined in the Vagrantfile or elsewhere. By default provisioners are executed when first upping the box.

```vagrant destroy```will delete the box in this environment but the Ubuntu base box is still in the cache and Vagrant is still here.

Provisioners can be provided inline or in an external file like we did.

``` 
  config.vm.provision "shell", inline: <<-SHELL

```

change to this for a pathed file

```
   config.vm.provision "shell", path: "provisioners/nginx-install.sh"
```
## Provisioner is only run the first time a box is started. So destroy and up if you modified provisioners so that doesn't work with reload.

There are otions to run on each boot, run :always.





