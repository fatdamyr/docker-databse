Vagrant.require_version ">= 1.6.3"
VAGRANTFILE_API_VERSION = "2"

WWW_ROOT = "/vagrant/html"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "boot2docker"

  config.vm.box = "parallels/boot2docker"

  
  #Network Setup
  config.vm.network "forwarded_port", guest: 80, host:80
  
  #Mount shared folders to the docker host OS
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provision :docker do |d|
  
    #Create Weblogic Server container
    #See https://github.com/oracle/docker/tree/master/OracleWebLogic
  
    
    #Load Apache HTTPD image and run container on port 80
    #/usr/local/apache2/htdocs/ is the webroot for this image so mount our files there
    # See https://registry.hub.docker.com/_/httpd/
    
    d.pull_images "httpd:2.4"
    d.run "httpd",
      image: "httpd:2.4",
      args: "-it --name webserver -p 80:80 -v '$WWW_ROOT:/usr/local/apache2/htdocs'"
      
  end
end