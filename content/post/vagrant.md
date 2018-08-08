+++
date = "2018-07-06T10:54:24+02:00"
draft = false
title = "This Hugo Blog in a Vagrant Environment"
slug = "this_hugo_blog_in_a_vagrant_environment"
tags = ["Vagrant","Hugo"]
image =  "images/vagrantdarter.jpg"
comments = false
share = true
menu= ""
author = ""
+++

Vagrant from Hashicorp is great way to abstract away from virtualization or infrastructure technology like Virtualbox, VMware, 
Microsoft HyperV, Cloud Providers etc. You just declare what you need and like magic everything is ready for use after some minutes.

Cutting to the chase here is my setup to edit this Blog. Of course I need Vagrant installed, but this is not a problem as I use it in
my everyday Job also.

	myboxname = "gabi"

	Vagrant.configure("2") do |config|
	  config.vm.box = "ubuntu/xenial64"
	  config.vm.hostname = myboxname
	  config.vm.box_check_update = false
	  config.vm.network "private_network", ip: "192.168.33.10"
	  config.vm.synced_folder "./data", "/data"

	  config.vm.provider "virtualbox" do |vb|
	     vb.gui = false
	     vb.name = myboxname
	     vb.memory = "512"
	     vb.linked_clone = true
	   end

	  #
	  # Provides updated git
	  #
	  config.vm.provision "git", type: "shell" do |s|
	    s.inline = <<-SHELL
	      apt-get update
	      apt-get install -y apt-transport-https ca-certificates software-properties-common
	      apt-get update
	      add-apt-repository -y ppa:git-core/ppa
	      apt-get install -y git
	      git --version
	      SHELL
	  end

	  #
	  # Install Hugo binary (no Go interpreter needed)
	  #
	  config.vm.provision "hugo", type: "shell" do |s|
	    s.inline = <<-SHELL
	      cd /usr/local/bin
	      HUGOVER=0.46
	      TARFILE=hugo_${HUGOVER}_Linux-64bit.tar.gz CHKFILE=hugo_${HUGOVER}_checksums.txt
	      wget -q --no-check-certificate https://github.com/gohugoio/hugo/releases/download/v${HUGOVER}/$TARFILE -O $TARFILE
	      wget -q --no-check-certificate https://github.com/gohugoio/hugo/releases/download/v${HUGOVER}/$CHKFILE -O $CHKFILE 
	      sha256sum --ignore-missing -c $CHKFILE || exit 1
	      tar xf $TARFILE
	      rm -f $TARFILE $CHKFILE
	      hugo version
	      SHELL
	  end
	end


What do you have?

+ Ubuntu Xenial with up to date Git installation & Hugo 0.46 binary.
+ Mounts the path `data` to `/data` where you can clone your blog.
+ You can edit the Blog from within the vagrant box or from the host machine using the mounted path.

See my notes [here](https://github.com/leonardossz/boxes) to get more details.

Thanks!

