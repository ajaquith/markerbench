---
title: "The DevOps Security Handbook: Building Security In With Chef, Part I"
authors:
 - arj
summary: This first post in a series about security and DevOps describes how to bootstrap development of a virtual test server.
date: 2013-10-01 16:18:00 -0500
tags:
  - cybersecurity
  - DevOps
image: /images/512px-Devops-toolchain.png
aliases:
  - /blog/2013/10/01/chef-starter/
---
{{< figure src="/images/512px-Devops-toolchain.png" title="Image copyright 2016 by Kharnagy, licensed under the Creative Commons Attribution-Share Alike 4.0 International license." >}}

# Introduction
This is the first in a series of posts about [Chef](http://www.opscode.com/chef/), an infrastructure automation platform. The goal of this series is to describe how to build a reasonably secure Apache web server. By using Chef, we can quickly and efficiently build identical web servers with assurance that they will work the same way, every time, and have the security properties we want.

You will build this server in stages. The server will ultimately contain the following elements:

* Apache 2 HTTP web server, with minimal modules and a virtual host defined for serving website content
* A limited user account whose home directory contains the website content. The account only accepts SSH remote logins that use public-key authentication. The Apache virtual host’s document root will point to a subdirectory of the account’s home
* A user group whose name matches the user account name, and which contains the user as its only member
* Hardened configuration with minimized services, synchronized time, intrusion prevention, and other security characteristics

For purposes of testing, the server will be spun up as a virtual machine on your local workstation. You will use VirtualBox VMs for this purpose.

This first post will describe how to set up a basic test infrastructure that uses Chef. You will set up the Chef workstation and server account, create an Apache server role and a test environment, set up a virtual machine, and build your first node. The web server will not do much, and it will not be especially secure — at least not initially. Subsequent posts will gradually add more security components. By adding security features gradually, you will learn how to use Chef. As a side effect, you will learn how Chef’s philosophy of “convergence” makes it easy to gradually massage your nodes into the states you want. This is important when adding Chef to servers that already exist.

# Getting started
In order to demonstrate how Chef works, you will need a virtual machine to play with. To create one, you will use Vagrant to instantiate a new VirtualBox VM. Our goal is to create a VM that you can boot and access on your laptop for testing purposes. After you do that, you will bootstrap it with Chef so that you can configure and manage it.

Some prerequisites. You will need to download and install:

* [VirtualBox](https://www.virtualbox.org) from Oracle, which creates and manages guest virtual machines.
* [Vagrant](http://www.vagrantup.com), which creates, manages, and destroys VirtualBox VM images from the command line.
* [Git](http://git-scm.com), the ubiquitous version-control system that will allow you to “check in” your Chef repository and manage its versions as you create the server.
* [Chef 11.x](http://www.opscode.com/chef/) workstation software, which is where all of the magic happens.
* [Ruby](https://www.ruby-lang.org/en/) 1.9.3 or higher

Chef works best on Unix- and Linux-based systems. I used a Mac to prepare this guide. But my instructions are largely platform independent; as long as you have a Linux- or BSD-based workstation, or a Mac, you should be in good shape.

OpsCode’s QuickStart guide does a fine job explaining how to do the initial preparatory steps in their [Workstation setup page](https://learnchef.opscode.com/quickstart/workstation-setup/). OpsCode recommends that you install a Ruby version manager. I use RVM myself, although the documentation (in the Advanced tab) recommends RBENV. Open up OpsCode’s QuickStart guide and do everything on Page 1. It should take you about 5 minutes.

Next, you need to create an [Enterprise Chef](http://www.opscode.com/enterprise-chef/) account, and download the starter package using the Enterprise Chef web interface.  [Page 2 of the  documentation page](https://learnchef.opscode.com/quickstart/chef-repo/) explains how to do this. The free version of Enterprise Chef supports up to five nodes, which is perfect for our purposes. After you sign up and create an account, create a new Organization and download the “Starter Kit” as described on QuickStart Page 2. Follow the instructions on this page all the way up to the “Create a Simple Cookbook” section. Once you have done that, you have configured your Chef workstation properly.

A word about the “Starter Kit.” The Starter Kit is a zipped bundle that contains a sample Chef repository directory structure, and crucially, a private key for the your workstation, which Chef calls a “client.” When you expand the Starter Kit,  it will unpack into a directory called `chef-repo`. This is your Chef repository, and you should move it somewhere useful. I put mine in `~/workspace`, which is where I keep all of my dev stuff, but you can put it anywhere you like.

Using the Chef workstation tools, you create and edit Chef roles, environments, cookbooks and other locally on your workstation. When you want to push new versions out to your nodes, you use Knife to upload them to the Enterprise Chef server. When you upload, Knife uses the client’s private key to authenticate with the Enterprise Chef server.

With the initial setup stuff out of the way, let’s start getting into the fun stuff.

# Creating sample server run-lists, roles and environments
I have found the OpsCode QuickStart documentation to be quite well-written. But it only gets you so far, and it leaves out some important steps for using Chef in a more serious way. Let’s take this opportunity to stray from the OpsCode documentation a bit and lay down some additional foundation-work for building the web server. In particular, let’s set up some initial run-lists, roles and environments for your test VM.

Some background. Chef “converges” nodes into their desired states by applying a ”run-list” of [recipes](http://docs.opscode.com/essentials_cookbook_recipes.html) to each node. The run-list of recipes (Apache2, NTPD, user creation, etc) that apply can be specified in several ways. The quickest and most direct way is to specify the node’s run-list of recipes when the node is initially bootstrapped with Chef; that is, when the Chef agent (`chef-client`) is initially installed on the node. Bootstrapping the node configuration is done using Knife, and the syntax looks like this:

    knife bootstrap tester.local --run-list "recipe[apt],recipe[apache2]" -E testing

I have omitted some of the syntax the sake of simplicity; don’t try running this. There are important concepts to understand here. The `bootstrap` command causes the `chef-client` application to be installed on the node. The `chef-client` is essentially an _agent_. It configures and installs software based on instructions (”recipes”) it receives from the Chef server. Notice the `run-list` parameter: it indicates that the APT and Apache2 recipes will be applied to node `tester.local`. What this means is that when `chef-client` is bootstrapped onto the node, the APT and Apache packages will be downloaded, installed and configured as well.

Notice also the `-E` parameter. This means that `tester.local` should be assigned to an environment called `testing`, which you will define in a minute. By ”environment,” Chef means a group of nodes that typically correspond to a stage of development, for example “testing,” “staging,” or “production.” Let's create the `testing` environment now. Type:

    knife environment create testing

…and type or paste the following JSON contents into the file:

    {
      "name": "testing",
      "description": "Test environment",
      "cookbook_versions": {
      },
      "json_class": "Chef::Environment",
      "chef_type": "environment",
      "default_attributes": {
      },
      "override_attributes": {
      }
    }

Nothing tricky here — just a simple JSON file with a few attributes in it. The `default_attributes` and `override_attributes` items can be used to supply variables to the recipes that are unique to the testing environment, for example, debug settings or dummy passwords. You will leave these blank for now because they don’t apply in this case.

As I mentioned, there are several ways to assign run-list items to nodes. Direct assignment of recipes during bootstrapping, shown in the edited `knife bootstrap` command above, is the easiest way. But that won't scale if you have multiple nodes that must be configured identically. It makes more sense, instead, to create a _role_, which allows common run-lists to be defined for groups of machines that do the same thing. Instead of bootstrapping with a specific run-list of recipes, you can bootstrap with roles. When you use a role, Chef looks up (dereferences, if you will) the run-list for the role and applies all of the recipes it contains, along with any custom attributes. You can think of roles as a type of pointer.

Let’s create a new role called `webserver`. In it you will add the components needed to run your website. Type:

    knife role create webserver

…and supply these contents:

    {
      "name": "webserver",
      "description": "Web server for my.org",
      "json_class": "Chef::Role",
      "default_attributes": {
      },
      "override_attributes": {
        "apache": {
          "listen_ports": [ "80" ]
        }
      },
      "chef_type": "role",
      "run_list": [
        "recipe[apt]",
        "recipe[apache2]",
      ],
      "env_run_lists": {
      }
    }

Notice that the `run-list` attribute contains the `apache2` cookbook, similar to what you used in the initial bootstrap command. The  `listen-ports` override attribute tells the `apache2` cookbook to configure Apache to listen just on port 80. You will learn more about override attributes in a future post. But if you are curious about how the cookbook works, and about the various attributes you can use to customize Apache’s configuration, see OpsCode’s [online decimation](http://community.opscode.com/cookbooks/apache2). Notice also the `apt` recipe; this is required because Debian’s APT package updater is how Apache is actually installed onto the node.

To bootstrap using roles instead of directly specifying recipes, you would use the following syntax (some details omitted):

    knife bootstrap tester.local --run-list "role[webserver]" -E testing

Again, don’t type this in, because it won’t work without some additional syntax; you will get to it soon enough.

Let's complete the initial Chef setup. So far, you have created a sample test environment called `testing`, and a sample server role called `webserver`. To complete the initial setup, you need to do two more things: download the actual cookbooks that Chef will apply to the node; and upload the cookbooks to the Chef server so that any nodes that are assigned it can get it. The cookbooks we need are `apt` (required to install Apache), and `apache2` (Apache itself).

To install the apache2 cookbook, type:

    knife cookbook site install apache2

This command looks up the `apache2` cookbook on the Opscode [community cookbook site](http://community.opscode.com) and causes it to be downloaded to your workstation. You will see a series of output messages showing the progress of the download, followed by a completion message when it succeeds. While you are at it, go ahead and install the `apt` cookbook too.

After downloading both, commit your current Chef repo to Git:

    git add .
    git commit -m "Added Apache and APT cookbooks."

Then upload your cookbooks to the Chef server:

    knife cookbook upload --all

It might seem a little strange to have to upload the cookbooks to the Chef server. After all, they are managed centrally from the community cookbook site. Why can’t roles simply reference the cookbooks stored there, instead of needing to make copies? Frankly, I am not too sure why this is the case. I suspect Chef works this way so that cookbooks and recipes can be hacked up when needed. Regardless, you must upload cookbooks to Chef server after you update them. If you don’t, the Chef client on any nodes you create will continue to use outdated recipes.

# Backing up Chef server data
Because you are using Enterprise Chef, your nodes, roles, environments and data bags are stored on the server — not locally. While I trust OpsCode to keep their servers up and available, I like to keep copies of important data on my client so that I have a record of them, and can version them with Git. You should, too.

To do that, you will need to install the `backup-export` Knife plugin, part of the [Knife Hacks](https://github.com/stevendanna/knife-hacks) package. Then, you should copy a specific plugin file from GitHub into our local Chef knife plugin cache in `~/.chef/plugins/knife`, creating the directory if necessary. A few quick commands should do the trick:

    mkdir -p ~/.chef/plugins/knife
    curl https://raw.github.com/stevendanna/knife-hacks/master/plugins/backup_export.rb > ~/.chef/plugins/knife/backup_export.rb

Change back to your `chef-repo` directory and issue the following command:

    knife backup export

You’ll see output similar to this:

    Backing up nodes
    Backing up nodes tester.local
    Backing up roles
    Backing up roles webserver
    Backing up data bags
    Backing up environments
    Backing up environments testing

By default, backups are stored in `.chef/chef_server_backup`. You can change this by modifying the `chef_server_backup_dir` entry in `.chef/knife.rb`, but there’s no obvious benefit to doing that here. It is sufficient simply to have them present in the Chef repo directory, because they can be checked into Git using the usual familiar `git add .` and `git commit` steps. Go ahead and do that now.

If you have gotten this far, your initial Chef setup is complete. Now, let’s create a test machine.

# Creating a virtual machine for testing
Change to your Chef repo directory. Create a new file `Vagrantfile` with these contents, or edit the existing one so that it matches this:

    # -*- mode: ruby -*-
    # vi: set ft=ruby :
    Vagrant.configure("2") do |config|
      config.vm.box = "opscode-ubuntu-12.04-i386"
      config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04-i386_provisionerless.box"
      config.vm.hostname = "tester.local"
      config.vm.define :tester do |t|
      end
      config.vm.network "private_network", ip: "192.168.56.2"
      config.vm.provider :virtualbox do |vb|
        vb.gui = false
        vb.name = "tester.local"
      end
    end

`Vagrantfile`’s job is to tell Vagrant how to set up the test VM. If you have used Vagrant before, you will notice that this `Vagrantfile` is shorter than the default file Vagrant supplies. Here's what it does:

* Downloads an Ubuntu 12.04 base box (essentially, a virtual machine image) from OpsCode’s repository on Amazon
* Creates a VirtualBox VM based on the machine image
* Gives the VM the network name `tester.local`. This is the name that the Unix command `hostname` will return when you log into it
* Names the VirtualBox machine `tester`. This is the name used to start, stop and delete the VM when using the VirtualBox command-line tools or the VirtualBox GUI.
Names the VirtualBox image directory `tester.local`. By default, VirtualBox names the image based on the directory that contains `Vagrantfile`, plus a timestamp suffix. The `vb.name` property inside the `config.vm.provider` block overrides the default so that it matches the host name.
* Configures the VM’s networking interface to use a private network address 192.168.56.2. This will allow us to start the VM and see it on our workstation, but the VM won’t be accessible from the outside.
* Specifies that when you boot the VM, it will be booted in headless mode; the VirtualBox GUI won’t be displayed.

That is all you need to instantiate a new VM on our workstation. Next, edit your workstation’s `/etc/hosts` file and add a line that points to the VM using the private IP address and name `tester.local`:

    192.168.56.2    tester.local

Great. Now, let’s go ahead and actually create the VM. From the command line in the same directory as `Vagrantfile`, type:

    vagrant up

Vagrant will look by default in the same directory for `Vagrantfile`, and having found it, will create the VM according to the contents of the file. You will see output similar to the following:

    Bringing machine 'tester' up with 'virtualbox' provider...
    [tester] Importing base box 'opscode-ubuntu-12.04-i386'...
    [tester] Matching MAC address for NAT networking...
    [tester] Setting the name of the VM...
    [tester] Clearing any previously set forwarded ports...
    [tester] Creating shared folders metadata...
    [tester] Clearing any previously set network interfaces...
    [tester] Preparing network interfaces based on configuration...
    [tester] Forwarding ports...
    [tester] -- 22 => 2222 (adapter 1)
    [tester] Booting VM...
    [tester] Waiting for VM to boot. This can take a few minutes.
    [tester] VM booted and ready for use!
    [tester] Setting hostname...
    [tester] Configuring and enabling network interfaces...
    [tester] Mounting shared folders...
    [tester] -- /vagrant

The entire process should take between 30 seconds to a minute if the base box is already cached on your workstation. If not, the first time you do `vagrant up` Vagrant will need to download the machine image from Amazon.

You can verify that the new test VM is up by pinging tester and verifying that it responds:

    Tweety:chef-repo arj$ ping tester.local
    PING tester (192.168.56.2): 56 data bytes
    64 bytes from 192.168.56.2: icmp_seq=0 ttl=64 time=0.582 ms
    64 bytes from 192.168.56.2: icmp_seq=1 ttl=64 time=0.638 ms
    …

Typing `vagrant status` will also indicate that the VM is up and running:

    Tweety:chef-repo arj$ vagrant status
    Current machine states:
    
    tester                    running (virtualbox)
    
    The VM is running. To stop this VM, you can run `vagrant halt` to
    shut it down forcefully, or you can run `vagrant suspend` to simply
    suspend the virtual machine. In either case, to restart it again,
    simply run `vagrant up`.

You can repeat this process as often as you like by destroying and recreating the VM:

    vagrant halt tester
    vagrant destroy tester

If you would like to verify that the VM is really up, you can SSH into the box using the username `vagrant` and password `vagrant`. You can also use the command `vagrant ssh` which does the same thing.

> Note: by default, base boxes used with Vagrant ship with a pre-installed SSH public/private key pair that is used for SSHing into VMs it creates. These base boxes also ship with default `vagrant/vagrant` credentials. This configuration is [not secure](http://stackoverflow.com/questions/14715678/vagrant-insecure-by-default). For testing purposes on your local workstation this should not be a problem, because we have configured the VM to use host-based networking. It cannot be accessed outside of the workstation. But production servers should not use Vagrant with its default configuration.

# Bootstrapping the virtual machine with Chef
So far, so good. You have successfully created a test virtual machine, but it isn't much good to us yet because it doesn’t have Chef on it. Until it does, you cannot manage it.

It is (finally!) time to “bootstrap” the VM using Knife. This installs the `chef-client` agent on the node, and registers the new node with the Chef server. Type in the following:

    knife bootstrap tester.local --ssh-user vagrant  --ssh-password vagrant --run-list "role[webserver]" -E testing --sudo

Viola! Assuming you did everything as described, Chef will SSH into the box, download and install Chef client onto it, and begin converging the node into its desired state; in this case, installing and configuring Apache.

Immediately after hitting Enter, a long list of output lines should appear. These should resemble the following:

    Bootstrapping Chef on tester.local
    tester.local --2013-09-29 03:20:41--  https://www.opscode.com/chef/install.sh
    tester.local
    tester.local Resolving www.opscode.com (www.opscode.com)...
    tester.local 184.106.28.82
    tester.local
    tester.local Connecting to www.opscode.com (www.opscode.com)|184.106.28.82|:443...
    tester.local connected.
    tester.local
    tester.local HTTP request sent, awaiting response...
    tester.local 200 OK

followed by

    tester.local Starting Chef Client, version 11.6.0
    tester.local
    tester.local resolving cookbooks for run list: ["apt", "apache2"]
    tester.local
    tester.local Synchronizing Cookbooks:
    tester.local
    tester.local   - apt
    tester.local
    tester.local   - apache2
    tester.local
    tester.local Compiling Cookbooks...

and then a series of lines that indicate that APT and Apache have been installed. The last lines indicate that Apache has been installed and restarted, and that the resources on the box have been updated:

    tester.local Recipe: apache2::default
    tester.local
    tester.local   * service[apache2] action restart
    tester.local
    tester.local
    tester.local     - restart service service[apache2]
    tester.local
    tester.local
    tester.local
    tester.local Chef Client finished, 28 resources updated
    tester.local

If you see output similar to this, and no errors, it means that you have successfully converged your first node. Congratulations! Excellent work.

You verify that the web server is up by firing up your browser to the address `http://tester.local`. It should return a “Forbidden” message because we have not actually provided any HTML pages for Apache to serve up. But that is evidence enough that Apache is actually working.

# Next: Adding security to the box
This post covered the basics of how to get going with Chef. You have installed the Chef workstation software and supporting components Git, Ruby and VirtualBox and Vagrant. You have created a sample role called `webserver` and assigned two sample recipes, `apache2` and `apt`, to it. You created a virtual machine called `tester` with the domain name `tester.local` and bootstrapped Chef onto it, placing it under Chef control.

In the [next post](/images/blog/2013/10/03/chef-2nd-course/), you will begin doing more useful work. I’ll describe how to fine-tune the Apache installation. We will also begin increasing the security of the machine.