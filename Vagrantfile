# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # box
  config.vm.box = "centos/7"

  # forwarded port mapping
  config.vm.network "forwarded_port", guest: 4000, host: 4000

  # synced folder
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"

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
    yum install nodejs -y
    
    # install GitBook
    npm install gitbook-cli -g
    
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
