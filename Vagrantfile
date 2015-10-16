# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "fedora22-virtualbox"
  config.vm.network "forwarded_port", guest: 8000, host: 8000
  config.vm.synced_folder ".", "/code"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    sudo dnf install -y tmux git vim-enhanced wget curl \
      gcc gcc-c++ \
      python3 python3-devel python3-pip python3-virtualenv \
      postgresql postgresql-server postgresql-devel

    sudo systemctl enable postgresql.service
    sudo postgresql-setup --initdb
    sudo systemctl start postgresql.service

    virtualenv-3.4 nitrate-env
    nitrate-env/bin/pip install -r /code/requirements.txt

    echo "Go to /code and happy hacking"
  SHELL
end
