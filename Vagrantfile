# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # box
  config.vm.box = "centos/7"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "public_network", ip: "192.168.33.10"

  # forwarded port mapping
  config.vm.network "forwarded_port", guest: 4000, host: 4000
  config.vm.network "forwarded_port", guest: 35729, host: 35729

  # Create a private network, which allows host-only access to the machine
  config.vm.network "private_network", type: "dhcp"

  # synced folder
  # config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  config.vm.synced_folder ".", "/vagrant", type: "nfs"

  # provisioning
  config.vm.provision :shell, inline: <<-SHELL

    # enable password authentication
    sed -i -e "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config
    service sshd reload

    # install Calibre
    yum install epel-release -y
    yum install qt-creator -y --enablerepo=epel
    yum install wget -y
    sudo -v && sudo wget --no-check-certificate -nv -O- https://raw.githubusercontent.com/kovidgoyal/calibre/master/setup/linux-installer.py | sudo python -c "import sys; main=lambda:sys.stderr.write('Download failed'); exec(sys.stdin.read()); main()"

    # install Node.js
    curl --silent --location https://rpm.nodesource.com/setup_6.x | sudo bash -
    yum install nodejs-6.9.2-1nodesource.el7.centos -y

    # install GitBook
    npm install gitbook-cli@2.3.0 -g

    # install genshin
    yum install p7zip -y
    cd ~
    mkdir genshin
    cd genshin/
    curl -O -L https://osdn.jp/downloads/users/8/8634/genshingothic-20150607.7z
    7za x genshingothic-20150607.7z
    mkdir -p /usr/share/fonts/genshin
    cp ./*.ttf /usr/share/fonts/genshin/
    chmod 644 /usr/share/fonts/genshin/*.ttf
    fc-cache -fv
  SHELL
end
