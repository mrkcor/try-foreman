# Introduction
With this project you have a playground to experiment with Foreman using Vagrant and VirtualBox (so install those before you get started!)

Follow these steps:

* Edit your local hosts file and add foreman.test as 192.168.1.2
* Perform a 'vagrant up'
* Connect to the vm that is to run foreman using: vagrant ssh foreman
* Run 'sudo foreman-installer' and write down the details in the output to make use of the web UI
* Run 'sudo puppet agent --test' before accessing the web UI

To enable you to work with the second vm do the following:

* Connect to it using: vagrant ssh bandit
* Run: sudo puppet agent --test
* Connect to the foreman vm with "vagrant ssh foreman" and sign the certificate for bandit with "sudo puppetserver ca sign --certname bandit.test", you can check for it first with "sudo puppetserver ca list"
* On bandit type "sudo puppet agent --test" again, from that point on you can configure the host in foreman

