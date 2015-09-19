# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.box = "debian/jessie64"
	
	# @see http://mxe.cc/#requirements
	config.vm.provider "virtualbox" do |v|
		v.memory = 2048
		v.cpus = 2
	end

	# @see http://mxe.cc/#requirements-debian
	config.vm.provision "shell", inline: <<-SHELL
		sudo apt-get update
		sidp apt-get install zip
		sudo apt-get install -y \
			autoconf automake autopoint bash bison bzip2 cmake flex gettext git g++ gperf intltool libffi-dev libtool libltdl-dev libssl-dev libxml-parser-perl make openssl p7zip-full patch perl pkg-config python ruby scons sed unzip wget xz-utils
		sudo apt-get install -y \
			g++-multilib libc6-dev-i386
		sudo apt-get install -y \
			libtool-bin
			
		git clone https://github.com/mxe/mxe.git
		cd mxe
		git checkout bec5b6c734756f981e98666ec52343277f4fbd2e
		echo "MXE_TARGETS := i686-w64-mingw32.static x86_64-w64-mingw32.static" >> settings.mk
		make gcc
		chown -R vagrant:vagrant .
	SHELL

end

