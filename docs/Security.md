# Securing the environment

Some default values can be dangerous if you expose your environment in hostile networks, here is some steps to harden your environment.  
See the [example pentestrc](../examples/secure-env.pentestrc) file.

## root password

The default root password is `toor`, we can change it with Chef:  
First we generate the password hash:
```
$ mkpasswd  -m sha-512 -S pentestenv -s <<< custom-password 
$6$pentestenv$2B8PIRYrG7XOMj8FQOHJ1hDMfniVVpgBVo70mes6mpTeNqApvCVUx6rS6gXojxLrsHqnwYavbJSjpd8HSUbHh1
```

Then, define the user password inside the `elite` cookbook:
```
kali:
  chef:
    recipes:
      - elite
    json:
      elite:
        users: [root]
        root:
          shell: /bin/bash
          password: $6$pentestenv$2B8PIRYrG7XOMj8FQOHJ1hDMfniVVpgBVo70mes6mpTeNqApvCVUx6rS6gXojxLrsHqnwYavbJSjpd8HSUbHh1
```

## Allowed SSH keys

The default allowed SSH private key to connect to the kali instance is public and can be found [here](https://raw.githubusercontent.com/Sliim/pentest-env/master/ssh-keys/pentest-env). Change it by:  

Generate a custom key:
```
$ ssh-keygen -f ssh-keys/custom-key
```
Copy your SSH public key (without type & label `cat ssh-keys/custom-key.pub|cut -d" " -f2`) and add it in your provisioning step:
```
kali:
  chef:
    recipes:
      - pentest-env::authorized_keys
    json:
      pentest-env:
        authorized_keys:
          root:
            - AAAAB3NzaC1yc2EAAAADA[....]RHazdIlN
```

After provisioning, the default private key will not be allowed to connect to the Kali instance, we need to use our new key:
```
kali:
  ssh:
    private_key_path: ssh-keys/custom-key
```

## Public network

Don't systematically connect your kali to public networks, only when required.

## Disable SharedFoldersEnableSymlinksCreate

Source: https://phoenhex.re/2018-03-25/not-a-vagrant-bug

It is recommended to disable the `SharedFoldersEnableSymlinksCreate` feature globally by setting the environment variable `VAGRANT_DISABLE_VBOXSYMLINKCREATE=1` in your profile.

All pentest-env targets which doesn't require provisionning (prebuilt boxes like vulnhub, metasploitable, etc..) disable the default vagrant shared folder. 
In case it is required, it can be re-enabled by defining a volume in the `pentestrc` resource file:
```
mytarget:
  volumes:
    .: /vagrant
```

All volumes defined in your `pentestrc` resources will automatically disable the `SharedFoldersEnableSymlinksCreate` feature (with the shared_folder's `SharedFoldersEnableSymlinksCreate: false` option).
