# docker-solo

## Get started

### Preparation

- Install [VirtualBox and Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- Install [Vagrant](https://www.vagrantup.com/downloads.html)
- Install [vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest)

```
vagrant plugin install vagrant-vbguest
```

### Boot up your solo server

Clone docker-solo project

```
git clone https://github.com/seandou/docker-solo.git
```

Run `vagrant up` to boot up docker server

```
cd docker-solo
vagrant up
```

Now you get a docker host, but it could not share files with your own system for missing [guest additions](https://www.virtualbox.org/manual/ch04.html)

You can install it automatically by set `config.vbguest.auto_update` to true or just install it manually:

```
vagrant vbguest --auto-reboot --no-provision
```
