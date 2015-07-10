# Strawberry
A [fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page) action that sends the banned IP addresses to [Threat Central](https://threatcentral.io/tc)

# Installation

- Make sure git is installed on your Linux server:
```bash

  sudo apt-get install -y git
```

- Clone the repository and create links:

```bash
  cd /usr/local
  sudo git clone https://github.com/amirkibbar/strawberry.git
  sudo ln -s strawberry fail2tc
  sudo ln -s ln -s /usr/local/fail2tc/fail2tc.conf /etc/fail2ban/action.d
```

- Edit fail2tc.properties, change the credentials to your Threat Central credentials
- Edit /etc/fail2ban/jail.conf, find line that says: banaction and add fail2tc beneath the default action, this is what it should look like:

```

  banaction = iptables-multiport
              fail2tc
```

- Restart fail2ban

