# How-to: Vagrant, Ansible, Composer
This is a training to standard tools to initialize projects environments, dependencies, configurations. You will create your own (minimal) LAMP stack using Vagrant and Ansible. Then get Drupal 8 running using Composer.

Goal for all FFW VN developers is to understand and follow a consistent method to setup project environments using: 
* Vagrant 
* Ansible
* Composer

When creating projects lead engineers will document all necessary dependencies, configurations, source and share as GIT repo with the team. Every project team member will clone the repo and develop in the same environment context to reduce risk of inconsistency and save time with tooling etc. 

### Prerequisites, Installations
* VirtualBox: https://www.virtualbox.org/wiki/Downloads
* Vagrant: https://www.vagrantup.com/downloads.html
* Ansible: `$ sudo apt-get install ansible`

### Provision a minimal LAMP stack
Clone this repository to your computer and launch a Virtual Box containing a minimal stack containing Ubuntu, Apache, MySQL, PHP, Composer. 

#### Vagrant
Go into your project folder (contains `Vagrantfile`) and run

`$ vagrant up`

`$ vagrant ssh`

#### Playbook
  ```
  tasks:
    - name: install apache
      apt: name=apache2 state=present
  ```
#### Composer
  ```
  {
    "name": "root/vagrant",
    "require": {
        "twig/twig": "^1.24"
    }
  }
  ```

### Install Drupal 8 with Composer

Manage your Drupal projects and all it's dependencies with composer has great benefits:
* Keep your projects consistent for all devs
* Avoid installing conflicting versions 
* Avoid backwards compatibility issues
* Only version control custom code (modules, themes). Everything else is managed with composer.json

Checkout this template for a [Composer managed Drupal 8 project:](https://github.com/drupal-composer/drupal-project)

Run command:
```
$ composer create-project drupal-composer/drupal-project:8.x-dev d8 --stability dev --no-interaction
```

Your Drupal code will be in `/d8/web/` and all other dependencies are in `/d8/vendor/`.
