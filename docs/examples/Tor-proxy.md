# Configure Kali linux with Tor & proxychains

## Pentestrc
This `pentestrc` will create and provision the `kali` instance to use proxychains as a tor proxy:
```
instances:
  - kali

kali:
  chef:
    recipes:
      - apt
    roles:
      - kali-base
      - tor-proxy
```

You can find this configuration file in [examples/tor-proxy.pentestrc](../../examples/tor-proxy.pentestrc).

Use it and run kali instance:
```
PENTESTRC=examples/tor-proxy.pentestrc vagrant up kali
```

Now you can use proxychains to send request througth Tor.

