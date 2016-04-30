# Openstack provider

See [installation instruction](Installation.md#openstack-provider) for requirements.

### Basic usage

You will need to setup your environnement to communicate with Openstack API. 

You can source your Openstack credentials and use them in your target. Provided instances/targets in pentest-env use your environment variables to configure Openstack provider.

Once you have configured your environment, you can create your instance:
```
> PENTESTRC=examples/openstack.pentestrc vagrant status
Current machine states:

kali                      running (virtualbox)
os-webgoat                not created (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`.

> PENTESTRC=examples/openstack.pentestrc vagrant up os-webgoat --provider=openstack
```

