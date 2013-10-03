---
title: The DevOps Security Handbook: Building Security In With Chef, Part II
author: Andrew Jaquith
date: 2013-10-03 13:30
categories:
- security
- DevOps
layout: post
comments: true
---
# Objectives
_This is the second in a series of occasional posts about security and DevOps. The ultimate goal of this series is to show how to build a reasonably secure Apache web server using the popular DevOps automation tool [Chef](http://www.opscode.com/chef/). The server I am describing how to build will be suitable for serving static content. Readers of this blog know that I am a fan of static blogging tools like [Octopress](http://octopress.org), which I use to generate this website._

If you read the [first post in this series](/blog/2013/10/01/chef-starter/), you learned how to set up the Chef workstation and server account. You created an Apache server role and a test environment; set up a virtual machine; and built your first node. In this post, I will show you how to create a new role called `base` that includes security enhancements to OpenSSH. You will also fine-tune Apache to remove non-essential modules.

<!-- more -->
 
# Tightening the Apache configuration
To recap, in the last post I described how to create a sample virtual machine called `tester.local`, onto which Chef installed the Apache 2 web server. If you were (as they say in the game-show world) “playing along at home,” you created a sample role called `webserver` that caused the `apache2` and `apt` packages to be installed on the node `tester.local`. You also bootstrapped the node so that it converged into the desired state.

As a refresher, let’s review a few details from last time. In your `chef-repo` directory, at the command line type:

    knife role edit webserver

You should see something that looks like this:

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
        "recipe[apache2]"
      ],
      "env_run_lists": {
      }
    }

This configuration works just fine, of course. It sets up Apache with the usual defaults. Lots of modules are enabled, and a default website is configured automatically. For demonstrations, that might be dandy. But in production situations, you should tighten up the configuration so that it is more secure. Security professionals know, as a general rule, that when something has fewer configured options, it is usually more secure. In that spirit, let’s:

* Minimize the attack surface by removing Apache modules we don’t need
* Decrease the amount of information “leaked” by the server by turning off server tokens and signatures
* Increase server performance by eliminating HTTP keep-alives
* Remove the default server website

If you have tried to do these things in the past, you probably wrote shell-code or some other kind of custom script. Or perhaps, like me, painstakingly hand-tuned the server and wrote down all of your specific hardening steps in a notebook in case you needed to do it again. The genius of Chef’s `apache2` cookbook is that you no longer have to do those things. The `apache2` cookbook recipes are cleverly written; they allow Apache to be heavily customized without requiring you to write code. Nearly everything that Apache does (or should _not_ do) can be controlled through _attributes_.

Attributes and their values can be defined in cookbooks via _attribute files_ and within recipes. They can also be defined for individual roles or environments. When attributes are defined in more than one place, those defined for specific environments beat those defined for roles, which in turn beat those defined in cookbooks.

Attribute values can also have multiple priorities. In reverse order of precedence, these are _default_, _force default_, _normal_, _override_, _force override_ and _automatic_ priority types. That is, the default attributes are used unless there are force-default, override, force-override or automatic values supplied somewhere; force-default attributes apply unless normal, override, force-override or automatic values are found, and so on. The precedence rules are fairly complex; OpsCode’s documentation [discusses them at length](http://docs.opscode.com/essentials_cookbook_attribute_files.html).

In this case, you will define a several _override_ attributes that will take precedence over the default values defined in the `apache2` recipes. When `chef-client` runs on the target node `tester.local`, these overridden values will be used in the various recipes to produce a more secure web server.

At the console, type:

    knife role edit webserver

In the editor screen, modify the `webserver` role so that it looks like this:

    {
      "name": "webserver",
      "description": "Web server for my.org",
      "json_class": "Chef::Role",
      "default_attributes": {
      },
      "override_attributes": {
        "apache": {
          "allow_override": "None",
          "contact": "nobody@example.com",
          "default_modules": [
            "alias",
            "cgi",
            "deflate",
            "dir",
            "log_config",
            "logio",
            "mime",
            "rewrite",
            "setenvif"
          ],
          "default_site_enabled": false,
          "directory_index": "disabled",
          "directory_options": "None",
          "ext_status": false,
          "keepalive": "Off",
          "keepaliverequests": "100",
          "keepalivetimeout": "15",
          "listen_ports": [
            "80"
          ],
          "serversignature": "Off",
          "servertokens": "Prod",
          "timeout": "120",
          "traceenable": "Off"
        }
      },
      "chef_type": "role",
      "run_list": [
        "recipe[apt]",
        "recipe[apache2]"
      ],
      "env_run_lists": {
      }
    }

The hash named `apache` (inside the `override_attributes` hash), contains the attributes that modify how the Apache is configured. If you are familiar with Apache configuration files, you can probably guess what many of the attributes do. In order, the override values tell Apache to:

* `allow_override`: Prevents `.htaccess` files placed in content directories from [overriding any directives](http://httpd.apache.org/docs/current/mod/core.html#allowoverride) already in place for the directory
* `contact`: Sets the [contact email address](http://httpd.apache.org/docs/current/mod/core.html#serveradmin) printed on Apache error pages to a bogus address
* `default_modules`: Restricts [Apache loadable modules](http://httpd.apache.org/docs/current/mod/mod_so.html#loadmodule) to just the few needed to server static content; in this case, `mod_alias`, `mod_cgi`, `mod_deflate`, `mod_dir`, two logging modules, `mod_mime` (MIME support), `mod_rewrite` (for URL re-writing) and `mod_setenvif` (useful for sending different responses based on browser types)
* `default_site_enabled`: Disables the default website
* directory_index: Disables [directory indexing](http://httpd.apache.org/docs/current/mod/mod_dir.html#directoryindex)
* directory_options: Disable all “[extra features](http://httpd.apache.org/docs/current/mod/core.html#options)” in directories, such as fancy indexing, symlink-following, multi-views, server-side includes and so forth
* `ext_status`: Disables [extended status](http://httpd.apache.org/docs/current/mod/core.html#extendedstatus) messages
* `keepalive`, `keepaliverequests` and `keepalivetimeout`: Disables HTTP [Keep-Alive](http://httpd.apache.org/docs/current/mod/core.html#keepalive) messages, which can cause performance to suffer in many cases
* `serversignature`: Removes [server signatures](http://httpd.apache.org/docs/current/mod/core.html#serversignature) from error messages
* `servertokens`: Minimizes the [response header field](http://httpd.apache.org/docs/current/mod/core.html#servertokens) to include just the webserver software (“Apache”) but not the version, OS or compiled-in options
* `timeout`: Increases the time the server [is allowed to respond to a request](http://httpd.apache.org/docs/current/mod/core.html#timeout) to 120 seconds
* `traceenable`: Removes support for the [HTTP TRACE](http://httpd.apache.org/docs/current/mod/core.html#traceenable) method

Of these attributes, the `default_modules` attribute is the most interesting because its value causes various Apache modules to be enabled or disabled. By default, the `apache2` recipe loads a huge number of modules. By overriding the defaults you can restrict what is loaded to a small subset.

Note that Apache always loads a few other modules regardless of the value of the `default_modules` attribute. These include authorization, content negotiation, timeout and status modules. But by keeping the list of modules small, you keep the server’s memory footprint smaller. You also get rid of features that aren’t needed in most websites and can be sources of risk, such as WebDAV support, LDAP authentication, proxying and so forth.

I do not claim to be an Apache expert by any means, but default settings in the list above are reasonably tight. Certainly, they are good enough to demonstrate how you can use attributes to customize how the Apache cookbook runs.

Now that you have created override attributes for the `web server` role, it is time to put them to use. Save and close the role editor; the contents will be saved to the Chef server.

SSH into the test VM and execute the node’s run-list again so that the new attribute values are applied. From the post from last time, recall that the Chef role `webserver` had been assigned to `tester.local`. All that you need to do, therefore, is run the client again. SSH into the box and elevate to `root`:

    vagrant ssh
    sudo su

and then:

    chef-client

You should see a dizzying rush of console messages, including many indicating that various Apache-related files are being modified. The run process should only take a few seconds. Assuming all recipes succeed, you will see a message at the bottom similar to the following:

    Recipe: apache2::default
      * service[apache2] action restart
        - restart service service[apache2]
    
    Chef Client finished, 31 resources updated

Congratulations; your Apache server is now just a little bit faster, and a little bit tighter. You did it solely by twiddling a few attributes, without having to write any code. Nice, huh?

# Creating a new role for server hardening
Let’s do some more attribute-twiddling. This time, your objective is to tighten the configuration of several common server components that reside on most servers: the SSH configuration, and the Chef client itself.

Download the cookbooks for SSH and the Chef client:

    knife cookbook site install openssh
    knife cookbook site install chef-client

Upload the cookbooks to the Chef server:

    knife cookbook upload --all

Create a second role. This role, called `base`, will be used by all servers and will include recipes that every server should use. Type:

    knife role create base

…and supply the following contents into the editor:

    {
      "name": "base",
      "description": "Essential recipes for securing every server",
      "json_class": "Chef::Role",
      "default_attributes": {
      },
      "override_attributes": {
        "openssh": {
          "server": {
            "allow_agent_forwarding": "no",
            "allow_tcp_forwarding": "no",
            "client_alive_count_max": "0",
            "client_alive_interval": "600",
            "ignore_user_known_hosts": "yes",
            "login_grace_time": "30s",
            "password_authentication": "no",
            "permit_root_login": "no",
            "rsa_authentication": "no"
          }
        }
      },
      "chef_type": "role",
      "run_list": [
        "recipe[openssh]",
        "recipe[chef-client::delete_validation]"
      ],
      "env_run_lists": {
      }
    }

The `openssh` recipe configures SSH on the machine. The override attributes above it configure the OpenSSH server daemon so that it uses sensible settings. Root logins are disabled, password authentication is disallowed; only public-key authentication is allowed. Session-forwarding is disabled, making the server unsuitable for use a “jump box.” (For more information on hardening SSHD, see the many [fine](http://www.faqs.org/docs/securing/chap15sec122.html) [articles](http://www.thegeekstuff.com/2011/05/openssh-options/) on the subject.) 

In addition to the SSH settings, notice the addition of the `chef-client::delete_validation` recipe. This recipe does something rather important from a security prospective. As discussed previously, Chef server communicates with its nodes and clients using public/private key pairs. When a new node is added, a shared “validation key” is copied to the new node. This is a standard 2048-bit RSA private key with a name similar to `organization-validator.pem`; it is stored in your Chef repository’s `.chef` directory. It is _not_ versioned by Git because `.chef/*.pem` is added to `.gitignore`, and it is obviously very sensitive. Anyone who obtained the validation key could conceivably join your Chef node set and gain access to the configuration data, recipes and more. Despite the sensitivity of this key, however, after the bootstrap operation completes, Chef inexplicably leaves it on the new node! It would be much nicer to remove it after the bootstrap.

For security reasons, you should remove the validation key after the initial bootstrap because it is not needed any more. The `chef-client::delete_validation` recipe does that. That is why it is in the run-list for the `base` role.

# Adding the `base` role to the server
After you define the `base` role, you need to apply it to the test VM `tester.local` by adding it to the node’s run list. At present, `tester.local` is only running recipes that are part of the `webserver` role. As you might expect, you can add to a node’s run-list by using `knife`. Type:

    knife node run_list add tester.local "role[base]"

You will see output similar to the following that confirms that the `base` role has been added to `tester.local`’s run list.

    tester.local:
      run_list:
        role[webserver]
        role[base]

SSH back into the test box (type `vagrant ssh` followed by `sudo su`). Run `chef-client` again.

You will see many messages scroll by indicating that the `/etc/ssh/sshd_config` and `/etc/ssh/ssh_config` files have been updated. By default, the Chef `openssh` cookbook configures these files with the default settings that ship with OpenSSH. Console output should look similar to the following:
    
    Recipe: openssh::default
      * package[openssh-client] action install (up to date)
      * package[openssh-server] action install (up to date)
      * service[ssh] action enable
        - enable service service[ssh]
    
      * service[ssh] action start (up to date)
      * template[/etc/ssh/ssh_config] action create
        - update content in file /etc/ssh/ssh_config from 265a26 to 74365c
            --- /etc/ssh/ssh_config	2012-04-02 11:49:30.000000000 +0000
            +++ /tmp/chef-rendered-template20131003-3037-n6ytk	2013-10-03 02:14:48.674543237 +0000
            @@ -1,53 +1,3 @@
    ...
      * template[/etc/ssh/sshd_config] action create
        - update content in file /etc/ssh/sshd_config from 33469d to 1ba1c4
            --- /etc/ssh/sshd_config	2013-05-11 06:10:17.805866080 +0000
            +++ /tmp/chef-rendered-template20131003-3037-6xl885	2013-10-03 02:14:49.114323240 +0000
            @@ -1,88 +1,14 @@
            -# Package generated configuration file
            -# See the sshd_config(5) manpage for details
            +# Generated by Chef for tester.local
    
    Recipe: openssh::default
      * service[ssh] action restart
        - restart service service[ssh]

You can verify that SSH has been reconfigured correctly by trying to SSH into `tester.local` using the default Vagrant account credentials (`vagrant`/`vagrant`). They should no longer work. However, typing the `vagrant ssh` command should still get you in. That is because the `vagrant ssh` authenticates using an embedded private key that is hardcoded into Vagrant. The public half of this key is an authorized key in the `vagrant` account’s list of public keys. (You can verify this yourself by examining the file `/home/vagrant/.ssh/authorized_keys` on `tester.local`. It shows one entry whose description reads “vagrant insecure public key.” How did it get there? Well, that is part of the ”contract” of building a [Vagrant-compatible base box](http://docs-v1.vagrantup.com/v1/docs/base_boxes.html).)

> Note: running the `openssh` recipe with the attributes as shown above can have adverse consequences on production nodes if you aren’t prepared. The recipe with the attributes as shown removes SSH `root` access. Unless you have another way of becoming `root` on the box, you might find yourself locked out! If your machine is a Vagrant machine, you can use the `vagrant ssh` command to become root. For non-Vagrant machines, you will need a non-root account that allows public-key logins and can `su` to `root`. You have been warned.

# Coming soon… adding a user account and web content directory
This post introduced the concept of using Chef to partially harden a web server. You reduced the number of loadable Apache modules to a minimum set, disabled unnecessary services and reduced the amount of useful information an attacker could obtain. You created a second role called `base` and assigned two recipes, `openssh` and `chef-client::delete_validation`. These recipes configure OpenSSH in a more restrictive manner by disabling password authentication, disabling root logins and preventing session forwarding. The `delete_validation` recipe removes the Chef validation key from the node after it is created, which removes a potential security risk.

In the next post, you will switch back to Apache. You will use Chef to create a non-privileged user whose home directory stores static HTML. This directory will served up by Apache as the default website. In keeping with the SSH configuration introduced in this post, the user account will be configured to use SSH public keys for authentication rather than passwords.
