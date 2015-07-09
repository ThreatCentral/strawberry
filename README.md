# Strawberry
A [fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page) action that sends the banned IP addresses to [Threat Central](https://threatcentral.io/tc)

# Installation

- Create the /usr/local/fail2tc directory
```bash

  sudo mkdir -p /usr/local/fail2tc

```
- Copy fail2tc and fail2tc.properties to this directory
- Edit fail2tc.properties, change the credentials to your Threat Central credentials
- Copy fail2tc.conf to /etc/fail2ban/action.d
- Edit /etc/fail2ban/jail.conf, find line that says: banaction and add fail2tc beneath the default action, this is what it should look like:
```

  banaction = iptables-multiport
              fail2tc
```
- Restart fail2ban

