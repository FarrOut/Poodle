# Poodle
Poodle (Personal Moodle) is an easy-to-deploy personal Moodle stack.

This project is aimed at making the complicated technical task of deploying a Moodle webservice as easy as possible for the average user who would prefer to focus their energy on creating and sharing helpful content with the world.

## Preparation

There are a few simple steps to get your home ready for your new Poodle.

### Install Dependencies
There are some pre-requisites which need to be in place in order to use this playbook.

#### System packages

Git - to checkout the Poodle repository.
Ansible - to execute the Poodle playbook.
Vagrant - to provision VMs to run and test your Poodle stack locally.

1. ``` apt install git ansible vagrant ```

#### Install vagrant-hostsupdater
Vagrant hostsupdater plugin - for local domain name resolution.

``` vagrant plugin install vagrant-hostsupdater ```

2. ### Checkout Source Code

You will need to copy the source code to your local machine, from where it will be executed by Ansible.

#### Checkout from GitHub
The easiest and recommended method is by cloning the repo from GitHub.

3. ``` git clone git@github.com:FarrOut/Poodle.git ```

#### Manual
If you prefer, you can also download and extract the source code manually.
