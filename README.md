OpenWrt msmtp
=============

This role installs and configures [msmtp](https://marlam.de/msmtp/) on [OpenWrt](https://www.openwrt.org/) targets.

Requirements
------------

This role has no special requirements on the controller.

It does, however, require a working [Python](https://www.python.org/) installation on the target system or [gekmihesg's Ansible library for OpenWRT](https://github.com/gekmihesg/ansible-openwrt) on the Ansible controller.

Role Variables
--------------

* `msmtp_default_config`  
  Set default configuration settings for all accounts.
  This variable must be a dictionary where the keys are msmtp configuration options and dictionary values are the respective configuration values.
  Refer to the [msmtp documentation](https://marlam.de/msmtp/msmtp.html) for valid options.
  Optional.
* `msmtp_accounts`  
  Set msmtp accounts and account-specific configuration.
  This variable must be a dictionary where the keys are msmtp account names and the dictionary values are dictionaries, with the same semantics as `msmtp_default_config`.
  Optional.
* `msmtp_package`  
  The name of the msmtp package to install.
  Usually either `msmtp` or `msmtp-nossl`.
  Defaults to `msmtp` if TLS is enabled in `msmtp_default_config` or `msmtp_accounts` and `msmtp-nossl` otherwise.

This role does not depend on any specific roles.

Example Configuration
---------------------

The following is a short example for some of the configuration options this role provides:

```yaml
msmtp_default_config:
  tls: true
  port: 587
msmtp_accounts:
  default:
    host: mail.oursite.example
    port: 465
    tls: true
    tls_starttls: false
    from: %U@oursite.example
    syslog: LOG_MAIL
  freemail:
    host: smtp.freemail.example
    from: joe_smith@freemail.example
    auth: on
    user: joe.smith
    password: secret123
```

License
-------

MIT
