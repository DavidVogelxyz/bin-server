bin-server
==========

`bin-server` is a collection of Bash scripts that should be on all Linux servers. This repo is often deployed in conjuction with [my dotfiles](https://github.com/DavidVogelxyz/dotfiles).

Usage
-----

Within the root of this project (`bin-server`) is a directory named `bin-server`. Create a symlink at `${HOME}/.local/bin/bin-server` that points to the *subdirectory* named `bin-server`.

Table of contents
-----------------

- [Usage](#usage)
- [Scripts](#scripts)
    - [certbot-renew](#certbot-renew)

Scripts
-------

### certbot-renew

Date created: 2026 Jan 3, Sat

`certbot-renew` was written to address issues with renewing Let's Encrypt SSL certificates on "servers running `ufw` with rules that normally prevent renewal".

`certbot-renew` solves this issue by temporarily opening the firewall after determining that an SSL certificate can be renewed. If the firewall is opened for any reason, a cleanup function is immediately trapped, such that the firewall is closed when the script exits. `certbot-renew` attempts to manage the firewall intelligently by only removing rules that it creates -- if the same rule already exists on the server, then `certbot-renew` does not remove that rule.

The repository includes an example cronjob that **should be added to the `root` user's crontab**, ensuring `certbot` is able to successfully renew SSL certificates when it identifies a certificate that is within the specified `RENEW_TIME` (default: 28 days).
