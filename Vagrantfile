# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Basic default configuration used for intial setup of box.
  # Please use if packaged boxes are unavailable or unwelcome
  # config.vm.box = "chef/debian-${target-os.version}"
  # config.vm.box_url = "https://vagrantcloud.com/chef/boxes/debian-${target-os.version}"

  # Box name and location
  config.vm.box = "${vagrant-box.name}"
  config.vm.box_url = "${vagrant-box.baseurl}/${vagrant-box.name}.box"

  # Basic network configuration
  config.vm.host_name = "${vagrant-box.name}"
  # Required for NFS to work, pick any local IP. Disabled due to errors with network configuration at Fedora 21 boxes.
  # Please enable at times and add a ", nfs: true" at the end of each folder sync
  config.vm.network :private_network, ip: '192.168.50.50'

  # Share some needed folders
  config.vm.synced_folder "${build.dir}", "${vagrant-build.dir}", nfs: true
  config.vm.synced_folder "${reports.dir}", "${vagrant-reports.dir}", nfs: true
  config.vm.synced_folder "${src.dir}", "${vagrant-src.dir}", nfs: true

  # Shell provisioning used for intial setup of box.
  # Please use if packaged boxes are unavailable or unwelcome
  # config.vm.provision "shell", path: "provision.sh"

  # Extend the timeout for initial connection
  config.vm.boot_timeout = 600

  config.vm.provider "virtualbox" do |vb|
    host = RbConfig::CONFIG['host_os']

    # Give VM 2Gb system memory & access to 2 cpu cores on the host
    mem = 2048
    cpus = 2

    vb.customize ["modifyvm", :id, "--memory", mem]
    vb.customize ["modifyvm", :id, "--cpus", cpus]
  end

  config.vm.define :"${vagrant-box.name}" do |t|
    end
end
