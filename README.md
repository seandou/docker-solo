# docker-solo

## Get started

### Preparation

- Install [VirtualBox and Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- Install [Vagrant](https://www.vagrantup.com/downloads.html)
- Install [vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest)

```
vagrant plugin install vagrant-vbguest
```

- Install [vagrant-env](https://github.com/gosuri/vagrant-env)

```
vagrant plugin install vagrant-env
```

### Initialize your solo server

Clone docker-solo project

```
git clone https://github.com/seandou/docker-solo.git
```

Run `vagrant up` to boot up solo server with provision

```
cd docker-solo
vagrant up
```

Now you get a docker host, but it could not share files with your own system for missing [guest additions](https://www.virtualbox.org/manual/ch04.html)

You can install it automatically by set `config.vbguest.auto_update` to true or just install it manually:

```
vagrant vbguest --auto-reboot --no-provision
```

### Dance with docker

After vm host is up, your can ssh to server by `vagrant ssh`.

Comment out lines for using docker easily:

```
# Run vagrant ssh as root user
config.ssh.username = 'root'

# Share $HOME/Projects between your os and solo server, you can edit the file with your favorite editor and run docker commands on solo server.
config.vm.synced_folder ".", "/vagrant", :disabled => true
config.vm.synced_folder ".", "/share"
config.vm.synced_folder "#{HOME}/Projects", "/root/projects"
```

## Useful tools

### [Docker Compose](https://docs.docker.com/compose/overview/)

```
curl -L https://github.com/docker/compose/releases/download/1.8.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

### [DockerUI](https://github.com/kevana/ui-for-docker)

```
docker run -d -p 9000:9000 --restart=always --name ui-for-docker --privileged \
  -v /var/run/docker.sock:/var/run/docker.sock \
  uifd/ui-for-docker
```

Browse `http://192.168.33.10:9000/` to visit it.
