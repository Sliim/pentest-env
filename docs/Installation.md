# Pentest-env Installation

Pentest-env works with Vagrant and Virtualbox. For installation instructions see:
- Vagrant: https://www.vagrantup.com/downloads.html
- Virtuabox: https://www.virtualbox.org/wiki/Downloads

Clone pentest-env repository and its submodules:
```
git clone https://github.com/Sliim/pentest-env.git
cd pentest-env/
git submodule init
git submodule update
```
Or in one line:
```
git clone https://github.com/Sliim/pentest-env.git --recursive
```

You can also use the [pentestenv](https://supermarket.chef.io/cookbooks/pentestenv) cookbook to install pentest-env.

## Chef provisioning
You will need `berkshelf` to download cookbook dependencies, you can install it with bundler:
```
bundle install --path=vendor/bundle
bundle exec berks vendor
```

Berkshelf will download cookbooks in `berks-cookbooks/` directory.

## Docker provider
To use Docker as a provider for pentest-env, you will need `docker` installed on your host:

- Docker: https://docs.docker.com/

## Openstack provider
Openstack cloud provider can be used to deploy vms, Vagrant needs a plugin to interact with Openstack API:
```
vagrant plugin install vagrant-openstack-provider
```
For more details see the project page: https://github.com/ggiamarchi/vagrant-openstack-provider
