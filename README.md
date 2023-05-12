# ec2-helper

Start and stop an EC2 instance by name and update ~/.ssh/config Host entry.

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
