# docker-solo

## Get started

### Preparation

- [VirtualBox and Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- [Ansible](http://docs.ansible.com/ansible/intro_installation.html#installation)
- [Vagrant 1.8.4](https://releases.hashicorp.com/vagrant/1.8.4/)
- [vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest)

```
vagrant plugin install vagrant-vbguest
```

- [Vagrant Host Manager](https://github.com/devopsgroup-io/vagrant-hostmanager) (optional)

```
vagrant plugin install vagrant-hostmanager
```

- [vagrant-env](https://github.com/gosuri/vagrant-env) (optional)

```
vagrant plugin install vagrant-env
```

### Initialize your solo server

Clone docker-solo project

```
git clone https://github.com/seandou/docker-solo.git
```

You can just use the default keys or generate rsa keys pair yourself:

```
ssh-keygen -t rsa -b 4096 -C "docker-solo" -f provisioning/roles/base/files/keys/id_rsa
```

Run `vagrant up` to boot up solo server with provision

```
cd docker-solo
vagrant up
```

### Dance with docker

After vm host is up, your can ssh to server by `vagrant ssh main`.

### Use shipyard

[Shipyard](http://shipyard-project.com/) is installed as default management tool, you can browse [http://192.168.10.10:8080/](http://192.168.10.10:8080/) to visit it. Default username is `admin` and password is `shipyard`.

## Other useful tools

### [Docker Compose](https://docs.docker.com/compose/overview/)

```
curl -L https://github.com/docker/compose/releases/download/1.8.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

### [DockerUI](https://github.com/kevana/ui-for-docker)

```
docker run -d -p 9000:9000 --restart=always --name docker-ui --privileged \
  -v /var/run/docker.sock:/var/run/docker.sock \
  uifd/ui-for-docker
```

Browse [http://192.168.10.10:9000/](http://192.168.10.10:9000/) to visit it.

## Resources

- [centos vagrant images](http://cloud.centos.org/centos/7/vagrant/x86_64/images/)
