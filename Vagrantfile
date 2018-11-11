# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
required_plugins = ["vagrant-hostsupdater", "vagrant-berkshelf"]
required_plugins.each do |plugin|
  unless Vagrant.has_plugin?(plugin)
    # User vagrant plugin manager to install plugin, which will automatically refresh plugin list
    puts "Installing vagrant plugin #{plugin}"
    Vagrant::Plugin::Manager.instance.install_plugin plugin
    puts "Installed vagrant plugin #{plugin}"
  end
end

Vagrant.configure("2") do |config|
  config.vm.define "jenkins-machine" do |jenkins|
    jenkins.vm.box = "ubuntu/xenial64"
    jenkins.vm.network "private_network", ip: "192.168.72.1"
    jenkins.hostsupdater.aliases = ["jenkins.vm"]
    jenkins.vm.provision "chef_solo" do |chef|
      chef.add.recipe "Jenkins::default"
    end
  end
end
