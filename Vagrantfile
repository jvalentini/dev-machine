# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/vivid64"
  config.vm.hostname = "dev-machine"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2560"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.groups = {
      "dev-machine-hosts" => ["dev-machine"]
    }
  end

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http = 'http://httpproxy.amicillc.com:8080'
    config.proxy.https = config.proxy.http
    config.proxy.no_proxy = 'localhost,127.0.0.1'
  end
end
