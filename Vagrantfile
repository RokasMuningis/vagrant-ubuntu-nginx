# Load hosts
require 'yaml'
hosts = YAML.load_file "hosts.yml"

# Configure vagrant machine
Vagrant.configure("2") do |config|

  # Declare OS
  config.vm.box = "ubuntu/xenial64"

  # Virtual-box settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1524"
  end

  # Server parameters
  config.vm.network "private_network", ip: "10.99.99.99"
  
  # Hostname
  config.vm.hostname = "svetaine.test"
  # Hosts / domains
  config.hostsupdater.aliases = hosts['list']

  # Configure shell
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

  # Provision
  config.vm.provision :shell, path: ".provision/prepare"

  # Folder syncing
  config.vm.synced_folder "./", "/srv/dev", :nfs => true
  config.bindfs.bind_folder "/srv/dev", "/srv/dev"
end
