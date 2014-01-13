Vagrant Web Development
=======================

This vagrant machine serves the purpose of providing an environment for my personal web development.

Pre-requisites
--------------

* [VirtualBox 2.*](https://www.virtualbox.org/wiki/Downloads) *Note* that _Vagrant is not compatible with version 3_
* [Vagrant](http://www.vagrantup.com/downloads.html)
* Ruby and RubyGem. Recommend using [rvm](http://rvm.io/)
* [Berkshelf](http://berkshelf.com/)
* [Git](http://git-scm.com/)

Setup
-----

* Clone the repository: $ git clone https://github.com/titomiguelcosta/VagrantWebDevelopment.git
* Download the chef recipes: $ berks install
* Start the vagrant machine: $ vagrant up

Alert
-----

In HP laptop, with Mint 16, I was getting an error that hardware virtualization was disabled.
I tried to disable on VirtualBox, go to System > Acceleration > Enable VT-x/AMD-V but no success.
The solution is to enable the virtualization on the BIOS. [Check the video tutorial](http://www.youtube.com/watch?v=lkLnsgghWRw)
