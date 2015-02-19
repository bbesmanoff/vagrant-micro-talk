## Vagrant in 5-ish Minutes

Brian Besmanoff  
:octocat: [bbesmanoff/vagrant-micro-talk][repo]

---

## What is Vagrant?
> Development environments made easy
> - https://vagrantup.com

---

## What Does That Mean?

---

## What Does That Mean?
* Development Environments - Where you write code
* made easy - (self explanitory)

---

## How Does That Help Me?
Quick, cheap, and ready-to-code VMs

---

## How Does That Happen?
Vagrantfile - a description file using a Ruby DSL

```ruby
# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "base"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,

```

---

## Some Cool Vagrant-isms

---

## Some Cool Vagrant-isms
### Provisioning
* Run Puppet, Chef, shell commands, etc

```ruby
  config.vm.provision 'shell', inline: 'sudo apt-get install -y apache2'
```

---

## A True Real-Life Example
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "hashicorp/precise32"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provision 'shell', path: 'vagrant_provisioning.sh'

end
```

---

## A True Real-Life Example
```
# Install dependencies
export DEBIAN_FRONTEND=noninteractive
apt-get -y update
apt-get -y install apache2 mysql-server php5 php5-mysql unzip

# Restart Apache for full PHP support
service apache2 restart

# Configure mysql
mysql -u root -e "CREATE DATABASE dvwa;"
mysqladmin -u root password "p@ssw0rd"

# Download/extract DVWA
wget -O dvwa.zip https://github.com/RandomStorm/DVWA/archive/v1.0.8.zip
unzip dvwa.zip

# Mount it at WEBROOT/dvwa
mv DVWA-1.0.8 /var/www/dvwa

# Create an XSS target
cat > /var/www/xss.html <<EOF 
<h1>PWNED</h1>
EOF
```

---

## A True Real-Life Demo

---

## Questions

[repo]: https://github.com/bbesmanoff/vagrant-micro-talk
