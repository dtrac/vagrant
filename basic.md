mkdir ~/vagrant/helloWorld ; cd ~/vagrant/helloWorld

# Create a Vagrantfile which will use Ubuntu 14.04
vagrant init ubuntu/trusty64

# Edit the Vagrantfile
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

# Many comments ommitted for brevity

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"
  
  # Define a VM name (as opposed to 'default') - for vagrant machine and VirtualBox gui
  config.vm.define "helloWorld"
  
  # Set hostname inside the VM
  config.vm.hostname = "helloWorld"
  
  # Default shared folder setting
  config.vm.synced_folder ".", "/vagrant"

  # Forward host's port 8080 to server's port 80
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  # Create a local file with content
  config.vm.provision "shell", inline: "echo 'Hello World!' > /vagrant/hello.txt"
  
  # Start a python simple web server
  config.vm.provision "shell", inline: "sudo python -m SimpleHTTPServer 80 &"

end
```

# Download the Ubuntu box (if not already downloaded) and start the instance
vagrant up --provision

# Check the file contents
