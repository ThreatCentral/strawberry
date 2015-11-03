# Strawberry
A [fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page) action that 
sends the banned IP addresses to [Threat Central](https://threatcentral.io/tc)

# Installing

- Make sure git is installed on your Linux server:
```bash

  sudo apt-get install -y git
```

- Clone the repository and create links:

```bash
  cd /usr/local
  sudo git clone https://github.com/ThreatCentral/strawberry.git
  sudo ln -s strawberry fail2tc
  sudo ln -s /usr/local/fail2tc/fail2tc.conf /etc/fail2ban/action.d
```

- Edit fail2tc.properties, change the credentials to your Threat Central 
credentials
- Edit /etc/fail2ban/jail.conf, find line that says: banaction and add fail2tc
beneath the default action, this is what it should look like:

```

  banaction = iptables-multiport
              fail2tc
```

- Restart fail2ban

# Upgrading

## Upgrading Manually

Assuming you installed fail2tc with git as described above, then to upgrade you
just need to update your git repository. Since the credentials are in the 
fail2tc.properties file, then this file has local changes which we need to first
stash, then pop:

```bash

  cd /usr/local/strawberry
  sudo git stash
  sudo git pull
  sudo git stash pop
```

## Upgrading with the fail2tc script

Starting with version 1.1 (check the header of the fail2tc script) it's also 
possible to upgrade by running:

```bash

  /usr/local/fail2tc/fail2tc --upgrade
```

You must first upgrade to version 1.1, after that upgrade will be possible by
running this script.

# Using fail2tc to block IP addresses from your Threat Central community

It is possible to block all IP addresses detected by fail2ban in your HP Threat
Central community. This means that you can benefit from other devices that share
their fail2ban banned IPs on their devices and with Threat Central.

To do this run a cron as root with:

```bash

  sudo fail2tc --ban
```

The above command will block all the IP addresses detected in your community in
the last 3 days. You can run this cron any time you see fit, we recommend doing 
it twice per day.

This functionality requires that nodejs would be installed on your machine:

```bash

  sudo apt-get install nodejs
```

# fail2ban configuration recommendations

We recommend you set the findtime to 3000 in the /etc/fail2ban/jail.conf file,
and, in addition we recommend you add the following regex to your
/etc/fail2ban/filter.d/ssh.conf:

```

  ^%(__prefix_line)sInvalid user .* from <HOST>s*$
```

The findtime increases the time between failures that is considered a brute
force attack. We've found that there are a lot of slow scanner out there that
purposly attempt to scan your servers very slowly to work around a fail2ban
installation.

The additional regex simply catches more ssh failures.

# License

&copy; Copyright 2015 Hewlett Packard Enterprise Development LP Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0) Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
