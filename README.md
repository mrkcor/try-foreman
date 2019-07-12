h1. Introduction
With this project you have a playground to experiment with Foreman using Vagrant and VirtualBox (so install those before you get started!)

Follow these steps:

* Edit your local hosts file and add foreman.test as 192.168.1.2
* Perform a 'vagrant up'
* Connect to the vm that is to run foreman using: vagrant ssh foreman
* Run 'sudo foreman-installer' and write down the details in the output to make use of the web UI
* Run 'puppet agent --test' before accessing the web UI
