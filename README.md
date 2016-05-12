# docker-osp-rally
Container to execute Rally tests against Openstack based on CentOS/Fedora

## How to start
Follow this steps to make easy the use of this container, I will asume that you already have docker installed:
- Download and prepare the environment
```
docker pull padajuan/docker-osp-rally
echo 'alias docker-rally="docker run --name rally -t -i -v ~/rally_home:/home/rally padajuan/docker-osp-rally"' >> $HOME/.bashrc
source ~/.bashrc
ln -s /path/to/rally_tests_folder ~/rally_home
```

- Execute Docker and start the container
```
sudo systemctl start docker
docker-rally
```

- Now start working with rally
```
rally-manage db recreate   ## This will create and populate the internal DB
rally deployment list      ## This shows you the deployment list
```

## How to change OS base
To change the OS base just modify the Dockerfile pointing to centos latest release and add this line:

```
FROM fedora:latest
...
RUN dnf update -y
RUN dnf epel-release -y
RUN dnf install -y git gcc libffi-devel python-devel openssl-devel gmp-devel libxml2-devel libxslt-devel postgresql-devel redhat-rpm-config wget python-pip which
...
...
```

Then, build the container and execute it ;)

Enjoy!!
