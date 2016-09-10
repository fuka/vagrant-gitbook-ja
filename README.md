# vagrant-gitbook-ja

Personal vagrant configuration for GitBook.

Japanese font(GenShinGothic) is installed, so you can generate a PDF including the Japanese.

## Requrements

- VirtualBox, tested with v5.1.4
- Vagrant, tested with v1.8.5

NOTE: Vagrant 1.8.5 has a authentication issue. Please apply the patch manually or use 1.8.4. see:[Authentication failure after inserting new key with Vagrant 1\.8\.5\. \[PATCH\] · Issue \#7610 · mitchellh/vagrant](https://github.com/mitchellh/vagrant/issues/7610)


## Virtual Machine Specifications

- OS : CentOS 7
- [GitBook](https://github.com/GitbookIO/gitbook) 3.2.0
- [calibre](https://calibre-ebook.com/) 2.67
- [Node\.js](https://nodejs.org/) 6.4.0
- [GenShinGothic](http://jikasei.me/font/genshin/) 1.002.20150607
