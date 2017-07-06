# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.box_check_update = false

  # config.vm.network "private_network", ip: "192.168.56.201"
  # config.vm.network "public_network"
  # config.vm.synced_folder "../data", "/vagrant_data"
  #config.vm.network "private_network", :ip => "192.168.56.201", :type => 'dhcp', :name => 'vboxnet0', :adapter => 2
  config.vm.network "private_network", :ip => "192.168.56.201", :type => 'dhcp', :name => 'vboxnet0'

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    vb.name = "test-ub"
  end

  config.vm.provision "shell", inline: <<-SHELL
#    sed -i 's/http:\/\/archive.ubuntu.com\//http:\/\/ftp.daumkakao.com\//' /etc/apt/sources.list
    sed -i 's@http://archive.ubuntu.com/@http://ftp.daumkakao.com/@' /etc/apt/sources.list
    apt-get update -qq && apt-get upgrade -y
    apt-get install -y git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
    apt-get install -y docker docker.io docker-compose
    # ruby environment
    git clone https://github.com/rbenv/rbenv.git /home/ubuntu/.rbenv
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> /home/ubuntu/.bashrc
    echo 'eval "$(rbenv init -)"' >> /home/ubuntu/.bashrc
    git clone https://github.com/rbenv/ruby-build.git /home/ubuntu/.rbenv/plugins/ruby-build
    # echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
    source ~/.bashrc
  SHELL
end
