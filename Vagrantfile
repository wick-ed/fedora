# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Basic default configuration
  config.vm.box = "chef/fedora-${target-os.version}"
  config.vm.box_url = "https://vagrantcloud.com/chef/boxes/fedora-${target-os.version}"

  # Basic network configuration
  config.vm.host_name = "${vagrant-box.name}"
  # Use NFS for shared folders for better performance
  config.vm.synced_folder "${basedir}", "${vagrant.basedir}"
  config.vm.synced_folder "${build.dir}", "${vagrant-build.dir}"
  config.vm.synced_folder "${reports.dir}", "${vagrant-reports.dir}"
  config.vm.synced_folder "${src.dir}", "${vagrant-src.dir}"

  # Shell provisioning
  config.vm.provision "shell", path: "provision.sh"

  # Extend the timeout for initial connection
  config.vm.boot_timeout = 1200

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
