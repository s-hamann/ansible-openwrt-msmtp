OpenWrt msmtp
=============

This role installs and configures [msmtp](https://marlam.de/msmtp/) on [OpenWrt](https://www.openwrt.org/) targets.

Requirements
------------

This role requires the [community.openwrt](https://github.com/ansible-collections/community.openwrt) collection on the Ansible controller.
As it exclusively uses modules from this collection, Python is *not* required on the target system.

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
* `msmtp_group`  
  The name of a system group to have read access to the msmtp config file.
  Only users in this group can use msmtp.
  This role creates the group if it does not exist on the target system.
  Optional.

Dependencies
------------

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
