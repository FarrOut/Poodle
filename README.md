# Poodle
Poodle (Personal Moodle) is an easy-to-deploy personal Moodle stack.

This project is aimed at making the complicated technical task of deploying a Moodle webservice as easy as possible for the average user who would prefer to focus their energy on creating and sharing helpful content with the world.

<img src="https://user-images.githubusercontent.com/8818608/91449653-a7ad5f00-e87b-11ea-8bc1-c892c382e507.jpg" alt="poodle" width="200"/>

<!-- ----------------------------------------------------------------------- -->

* [Poodle](#poodle)
   * [Preparation](#preparation)
      * [Install Dependencies](#install-dependencies)
         * [System packages](#system-packages)
         * [Install vagrant-hostsupdater](#install-vagrant-hostsupdater)
      * [Checkout Source Code](#checkout-source-code)
         * [Checkout from GitHub](#checkout-from-github)
         * [Manual](#manual)
   * [Usage](#usage)
      * [Local](#local)
         * [Deploying with Vagrant](#deploying-with-vagrant)
         * [Accessing Web Service](#accessing-web-service)
      * [Summary of Deployment Steps](#summary-of-deployment-steps)
      * [Custom Deployment Environment](#custom-deployment-environment)
   * [Healthchecks](#healthchecks)
      * [Step into Vagrant machine](#step-into-vagrant-machine)
      * [Display Docker process info](#display-docker-process-info)
   * [Future Work](#future-work)
      * [Multiple nodes](#multiple-nodes)
         * [Scaling](#scaling)
         * [Load Balancing](#load-balancing)
      * [Microservices](#microservices)
         * [Persistance](#persistance)
         * [Moodle Application](#moodle-application)
      * [Issue Board](#issue-board)
   * [Conclusion](#conclusion)

<!-- ----------------------------------------------------------------------- -->

## Preparation

There are a few simple steps to get your home ready for your new Poodle.

### Install Dependencies
There are some pre-requisites which need to be in place in order to use this playbook. Remember to elevate privileges with _sudo_ where necessary.

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

## Usage

### Local

#### Deploying with Vagrant

A local stack can be easily spun up using Vagrant, from the root of the repository.

![vagrant_up](https://user-images.githubusercontent.com/8818608/91446256-85b1dd80-e877-11ea-89af-78200e0add34.gif)

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

#### Accessing Web Service

It takes about a minute for the containers that form the stack to spin up, then you may access the web service from the web browser of your choice. Except IE (the poodle buried it).

Vagrant defines a name resolution entry, _poodle.local_, in your local machine to point to the stack.

Enter:

_poodle.local/_

in your browser.

![web](https://user-images.githubusercontent.com/8818608/91446744-21434e00-e878-11ea-8a23-b49eeeaf439e.gif)

Please note:
Because the SSL certifate generated is self-signed your browser will present a warning message to this effect. Because we trust Poodle's certificate (after examining this source code) please bypass this warning and proceed.

### Summary of Deployment Steps
For your convenience, here is an ordered list of commands which you need to execute.

```
apt install git ansible vagrant
vagrant plugin install vagrant-hostsupdater
git clone git@github.com:FarrOut/Poodle.git
cd Poodle/
vagrant up

```

### Custom Deployment Environment

One might also choose to deploy to a set of remote hosts, such as cloud VMs.

Included is an example of an [inventory](https://github.com/FarrOut/Poodle/blob/feature/documentation/inventory.yml) file. Keep the groups as is, but add your desired host nodes with their relevant IP addresses.

To deploy to remote hosts, we will need to exclude Vagrant and execute Ansible directly. Like so:

```

ansible-playbook -i inventory.yml provisioning/personal-moodle-stack-playbook.yml -K

```

## Healthchecks

Diagnostic healthchecks are transparent to the user as they work under the hood of Docker Swarm. However, you may like to manually inspect the state of the health of your stack.

### Step into Vagrant machine

If your stack is deployed locally via Vagrant, you will first need to step into the relevant Vagrant machine.

```

vagrant ssh [machine-name]

```

![vagrant ssh](https://user-images.githubusercontent.com/8818608/91447791-5bf9b600-e879-11ea-93e6-5465ee6b4cdc.gif)

### Display Docker process info

```

watch -n 1 'sudo docker ps'


```

Under the STATUS column, our containers should hopefully all read 'healthy'.

![docker ps](https://user-images.githubusercontent.com/8818608/91448185-dcb8b200-e879-11ea-8d69-f1564d0e66f2.gif)

## Future Work

Poodle is still a young pup with much training still needed. Here is a summary of what still needs to be done to get the Poodle well-trained and obedient as well as which direction our Poodle is heading.

### Multiple nodes
At the moment, the entire Poodle stack is deployed to a single machine. This is fine for now, but we'd really like to implement some clustering across multiple machines. Fortunately, the stack is already deployed on a Docker Swarm which needs a little more configuration tweaking to get working.

#### Scaling
Additional containers and worker nodes should also give us the benefit of elastic horizontal scaling of our application nodes.

#### Load Balancing
Multiples nodes means that our Nginx gateway can be configured for load-balancing.

### Microservices
The original intention was to implement a Microservices architecture. At the moment we only have an Nginx container running as a gateway. Luckily, we are already deploying a Docker Swarm so deploying more services to the existing stack shouldn't be too difficult.

#### Persistance
One such microservice is a database container to persist our data.

#### Moodle Application
The purpose of Poodle. Start off by deploying a vanilla Moodle container, then customise it to the flavour that suits our needs.

### Issue Board
For a more detailed list of outstanding issues which are begging to be seen to, please visit the [issue board](https://github.com/FarrOut/Poodle/issues).

## Conclusion

I hope you enjoy using Poodle as much as I have enjoyed developing it -- Please feel free to contribute to the effort!
