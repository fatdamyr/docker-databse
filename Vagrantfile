Vagrant.require_version ">= 1.6.3"
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "boot2docker"

  config.vm.box = "parallels/boot2docker"

  
  #Network Setup
  #config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network "forwarded_port", guest: 80, host:80

  #config.vm.synced_folder ".", "/vagrant", type: "nfs"

  config.vm.provision :docker do |d|
    
    #Load Apache HTTPD image and run container on port 80
    # See https://registry.hub.docker.com/_/httpd/
    
    d.pull_images "httpd:2.4"
    d.run "httpd",
      image: "httpd:2.4",
      args: "-it --name webserver -p 80:80"
  end
end