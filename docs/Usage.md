# Usage

All you need to know is basic vagrant commands :)

Move into `pentest-env` directory and:
```
> cd /path/to/pentest-env
> vagrant status
Current machine states:

kali                      not created (virtualbox)
dvwa                      not created (virtualbox)
```

Kali linux is the primary VM on pentest-env, so, the command to run it:
```
> vagrant up 
```

To run others instances / targets you need to specify their name:
```
> vagrant up dvwa
```

## Other providers
Pentest-env support following providers: 
- [Docker](Docker.md)
- [Openstack](Openstack.md)
