Vagrant.configure("2") do |config|

  # Just configured for VirtualBox only. Extend for other systems if needed.
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
	vb.cpus = 2
  end

  config.vm.box = "ubuntu/xenial64"
  
  # map the current folder into VM
  config.vm.synced_folder ".", "/vagrant", type: "rsync", disabled: true
  config.vm.synced_folder ".", "/aubio-host/", type: "virtualbox"
    
  config.vm.provision "shell", run: "always", inline: <<-SHELL
    # update the system and needed packages
    apt-get update
	apt-get upgrade -y
	apt-get install -y git subversion curl cmake make pkg-config unzip python zip gcc-mingw-w64

	# create aubio folder and copy aubio sources
	mkdir -p /aubio/
	cd /aubio/
	cp -Rfv /aubio-host/src_to_build/* ./

	# run aubio mingw build script
	./scripts/get_waf.sh
	bash ./scripts/build_mingw

	# copy results to host
	cp $(find . -name "aubio-*.zip*") /aubio-host/out/
  SHELL

end
