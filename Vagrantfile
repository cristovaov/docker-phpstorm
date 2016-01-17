# -*- mode: ruby -*-
# # vi: set ft=ruby :
dir = File.dirname(File.expand_path(__FILE__))

require 'yaml'
set = YAML.load_file("#{dir}/Vagrant.yaml")

Vagrant.configure(2) do |config|
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
  config.vm.define set['Project']['name'] do |project|
    project.vm.box = set['Project']['vagrant_box']
    project.vm.provider "virtualbox" do |vb|
      vb.name = set['Project']['name']
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
    project.vm.network "private_network", ip: set['Project']['box_ip']
    project.vm.hostname = set['Project']['hostname']
  end
end
