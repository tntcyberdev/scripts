# Minimal LAMP stack

Clone this repository to your computer and launch a Virtual Box containing a minimal stack containing Ubuntu, Apache, MySQL, PHP, Nodejs, NPM, Git, Composer. Go into your project folder (contains Vagrantfile) and run

`$ vagrant up`

`$ vagrant ssh`

### Vagrantfile configs
  `config.vm.box = "ubuntu/trusty64" `

  find more boxes at https://atlas.hashicorp.com/search.

using a specific IP:

  `config.vm.network "private_network", ip: "192.168.33.10" `

shared folder:

  `config.vm.synced_folder "./docroot", "/var/www/html" `


Inline Shell provisioning:

```
config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y apache2
    sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt
    sudo apt-get install -y php5-gd
    sudo apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql

#drush install
    sudo php -r "readfile('http://files.drush.org/drush.phar');" > drush
    sudo chmod +x drush
    sudo mv drush /usr/local/bin
    # http://docs.drush.org/en/master/install/

#nodejs install
    sudo apt-get install -y nodejs
    sudo apt-get install -y npm

SHELL
```


### Vagrant commands:
* vagrant up
* vagrant provision
* vagrant ssh
* vagrant reload
* vagrant halt
* vagrant destroy