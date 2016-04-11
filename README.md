# lago-tutorial
This repository contains the default files for creating Lago environment. 

In this tutorial you will learn how to set up a custom virtual environment with Lago.
The virtual environment will be used as an infrastructure for your application, so you can run tests
in order to check the functionality of your application, without the overhead of setting up an infrastructure.

This tutorial will be “hands on”, and will take you through the process of creating, running and deploying the environment.

Lago environments are flexible and can be used for all different kinds of tasks. For keeping things simple I will focus on one scenario, although you will get the ability to create your own custom environment.
We will use only the basic mandatory commands of Lago, for further reading please advise: 
[Lagos Hompage](http://lago.readthedocs.org/en/latest/index.html)

#### Prerequisites:

Install Lago - follow [this](http://lago.readthedocs.org/en/latest/README.html) tutorial for more information


#### The scenario:

Create a Lago environment which will consist of three virtual machines that will host Jenkins infrastructure.

#### The VMs:

* host0 – Jenkins slave.
* host1 – Jenkins slave
* server – Jenkins server.

#### The network:

All the VMs will connect to the same virtual network .

#### Creating the working directory:

In order to create a working directory, clone the following repo:

https://github.com/gbenhaim/lago-tutorial

#### What is in the repository?

* init.json.in – This is the file which describes the structure of our environment: the specification of the vms, networks, the path and name of the deployment scripts for each vm.

* presets -  This directory contains presets for common enviornments.

* templates-repo – This directory contains .json files which specify the template repository that should be used. (The templates repository is the place from which the base “qcow2” virtual disks will be copied from).

* deployment-scripts – This directory contains the deployment scripts for each vm.

#### Editing init.json.in

The init.json.in is where we need to describe our environment e.g vms and network, so Lago can create them for us.

//TODO: elaborate about the different features and values that can be specified within the file.


#### Creating The Environment

From within the repo run:

```
lago init --template-repo-path=templates-repo/office.json lago-work-dir init.json.in
```

#### Deploy the VMs

cd into /lago-work-dir.
This command will turn on the vms:
```
lago start
```
And for a specific vm named "server":

```
lago start server
```

This command will run the deployment scripts (from within the vms) that were specified
in the init.json file:
```
lago ovirt deploy
```

### Interacting with the VMs

Lago allows you to connect to the vms with ssh.
for exmaple, if we have a vm named "server" we will use the following:

```
lago shell server
```

### Getting the state of the environment

You cae get information about the state of the enviorment with:

```
lago status
```

### Shutdown the environment

In order to send a shutdown signal to the machines we will use:

```
lago stop
```

And for a specific vm named "server":

```
lago stop server
```


