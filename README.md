# Poodle
Poodle (Personal Moodle) is an easy-to-deploy personal Moodle stack.

This project is aimed at making the complicated technical task of deploying a Moodle webservice as easy as possible for the average user who would prefer to focus their energy on creating and sharing helpful content with the world.

* [Table of Contents](#table-of-contents)
   * [Preparation](#preparation)
      * [Install Dependencies](#install-dependencies)
         * [System packages](#system-packages)
         * [Install vagrant-hostsupdater](#install-vagrant-hostsupdater)
      * [Checkout Source Code](#checkout-source-code)
         * [Checkout from GitHub](#checkout-from-github)
         * [Manual](#manual)
         * [Summary](#summary)
   * [Usage](#usage)

## Preparation

There are a few simple steps to get your home ready for your new Poodle.

### Install Dependencies
There are some pre-requisites which need to be in place in order to use this playbook. Remember to elevate priveleges with _sudo_ where necessary.

#### System packages

Git - to checkout the Poodle repository.
Ansible - to execute the Poodle playbook.
Vagrant - to provision VMs to run and test your Poodle stack locally.

``` apt install git ansible vagrant ```

#### Install vagrant-hostsupdater
Vagrant hostsupdater plugin - for local domain name resolution.

``` vagrant plugin install vagrant-hostsupdater ```

### Checkout Source Code

You will need to copy the source code to your local machine, from where it will be executed by Ansible.

#### Checkout from GitHub
The easiest and recommended method is by cloning the repo from GitHub.

``` git clone git@github.com:FarrOut/Poodle.git ```

#### Manual
If you prefer, you can also download and extract the source code manually.

#### Summary
For your convenience, here is the list of commands which you need to execute, in order.

```
apt install git ansible vagrant
vagrant plugin install vagrant-hostsupdater
git clone git@github.com:FarrOut/Poodle.git

```

## Usage

A local stack can be easily spun up using Vagrant, from the root of the repository.

To build a new stack of VMs:

``` vagrant provision ```

Launch stack:

``` vagrant up ```

Launch a stack, and reprovision:

``` vagrant up --provision ```

Shutdown VMs

``` vagrant suspend [machine-name] ```
E.g. vagrant suspend boss

Delete VMs

``` vagrant suspend -f [machine-name] ```
E.g. vagrant destroy -f boss
