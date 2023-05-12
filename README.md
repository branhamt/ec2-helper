# ec2-helper

Start and stop an EC2 instance by name and update ~/.ssh/config Host entry.

## What is this for?

When an EC2 instance with a public IP address is shut down, the IP address changes once it is booted again. I wanted to be able to reconfigure my ~/.ssh/config with the new IP. [I did not want to use AWS ENI or Elastic IP](https://www.swe-devops.com/posts/manage-ec2-ssh-config-bash/).

Additionally, I'm using these scripts with EC2 instances that shut down on inactivity. These scripts are a quick way to start or stop an instance and update the IP address on a reboot.

## Commands

**Start an EC2 instance.**

```bash
ec2 start myserver
```

**Stop an EC2 instance.**

```bash
ec2 stop myserver
```

Use tab completion to get server names:

```bash
ec2 stop mys<TAB>
```

...will autocomplete to:

```bash
ec2 stop myserver
```

...when you have myserver as a Host name in your ~/.ssh/config.


## Installation

Clone this repo.

Do this in your .bashrc:

```bash
PATH=$PATH:/path/to/ec2-helper
. /path/to/ec2-helper/ec2_bash_completion
```

This will:

- Put /path/to/ec2-helper in your PATH so you can call it from anywhere.
- Source the autocompletion script to autocomplete host names from your ~/.ssh/config.

## Caveats

The script has a little brittleness based on your ssh config.

It relies on a grep command that expects Hostname to be in a 4 line block afterthe Host line in your ~/.ssh/config.

This will succeed (highlighted lines are grepped):

```
Host somehost
    IdentityFile ~/.ssh/somehost.pem
    IdentitiesOnly yes
    User ubuntu
    Hostname some.ip.addr.ess
    StrictHostKeyChecking no
    UserKnownHostsFile ~/.ssh/known_hosts_test
```

This will fail (highlighted lines are grepped):

```
Host somehost
    IdentityFile ~/.ssh/somehost.pem
    IdentitiesOnly yes
    User ubuntu
    StrictHostKeyChecking no
    UserKnownHostsFile ~/.ssh/known_hosts_test
    Hostname some.ip.addr.ess
```
