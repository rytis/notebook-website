---
title: "Building CentOS Machine With Vagrant and VeeWee"
date: 2011-11-29T07:21:33+01:00
draft: false
---

This is more of a quick checklist for building a CentOS box with Vagrant and VeeWee than a real blog post.

### Prerequisites

- Oracle VirtualBox installed
- Vagrant installed (`sudo gem install vagrant`)
- VeeWee installed (`sudo gem install veewee`)
- CentOS 6.0 i386 DVD ISO downloaded from one of the mirrors listed in <http://isoredirect.centos.org/centos/6/isos/i386/>

### Building a CentOS box

- Create working directories and copy the ISO image

```bash

$ mkdir -p ~/vagrant/centos60build/iso
$ cd ~/vagrant/centos60build
$ cp __PATH_TO_THE_ISO_IMAGE__ ./iso/

```

- Create a box definition

```bash

$ vagrant basebox define centos60 CentOS-6.0-i386

```

- Make any changes you need to the definition file in `definitions/centos60/definition.rb`. Make sure the name of the ISO and its MD5 are correct.
- Adjust postinstall and kickstart files if you need to
- Kickstart a Virtual Machine with CentOS 6.0 (this is going to take a while)

```bash

$ vagrant basebox build centos60

```

- Check that it is functional

```bash

$ vagrant basebox validate centos60

```

- Build a Vagrant box file

```bash

$ vagrant basebox export centos60

```

- Import it to Vagrant

```bash

$ vagrant box add centos60 centos60.box

```

### Using your new box

To spin off a new instance, run the usual Vagrant commands:

```bash

$ vagrant init centos60
$ vagrant up
$ vagrant ssh

```

Check out [these instructions](../../../../2011/04/30/use-fabric-on-vagrant-instances) on how to set up Fabric so that it can talk to your Vagrant VM instances.

