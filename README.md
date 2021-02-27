

freeradius
=========

Role that installs and configures freeradius 3 on Ubuntu. It will remove any unmanaged configuration to ensure a clean setup of freeradius.

This role might need some work for your situation! I will try to add soms functionality when i find the time for it.
Some examples that are not (yet) included in the role and will be cleaned up (deleted).

- proxy config
- trigger config
- templates config
- panic.gdb
- dictionary config
- policy.d

Other stuff that could be better:
- sites should be templated
- other os releases could be added

The role uses a single dict for configuration. This is so that all defaults will be overridden if you create your own configuration, wich i strongly recommend. Use ansible merge strategy if you would like to configure the role on multiple levels such as the defaults.


Requirements
------------
None

Role Variables
--------------

| var_name | required | default | description |
| -------- | -------- | ------- | ----------- |
| freeradius.config | yes | see below | this is a dict dat defines configuration for all available options |
| freeradius.config.*.disabled | no | - | disables the config |
| freeradius.sites | yes | see below | this is a dict that configures the sites, undefined sites will be removed |
| freeradius.modules | yes | see below | this is a dict that configures the modules, undefined and disbaled modules will be removed |


Example config dict
-------------------
```
---
freeradius_ssl_dh: |
    -----BEGIN DH PARAMETERS-----
    MIGHAoGBAOi4jKRQpxaycsaK1GYXrp4E1rnL2YL/5a7xka+vy8+5EMXP3uldS+DX
    +xv/9r3kMGlnsw0QSib0d3+Vq/Ph4x5fKCKcsYcc1PYQZPBDKKXFpWAKTQ5F7CzQ
    PtFFk/7BFclkeSNv0YjshE4haWiCeufs8dDBDlpzYklue1lKKKiTAgEC
    -----END DH PARAMETERS-----
freeradius:
  config:
    dictionary:
      filename: "dictionary"
      disabled: true  # not configured by default
    radiusd:
      filename: "radiusd.conf"
      disabled: false
      thread_pool:
        start_servers: 5  # 5 by default
        max_servers: 64  # 32 by default
        min_spare_servers: 3  # 3 by default
        max_spare_servers: 10  # 10 by default
        max_requests_per_server: 0  # 0 by default
        auto_limit_acct: yes  # no by default
        max_queue_size: 65536  # 65536 by default
  sites:
    default:
      config_file: "sites/default"
    inner-tunnel:
      config_file: "sites/inner-tunnel"
  modules:
    always: []
    attr_filter: []
    cache_eap: []
    chap: []
    date: []
    detail: []
    detail.log: []
    digest: []
    dynamic_clients: []
    eap:
      config_file: "modules/eap"
    echo:
      disabled: true  # enables execution of local commands
    exec: []  # enables execution of local commands
    expiration: []
    expr: []
    files: []  # required. tbv Livingston-style 'users' file
    linelog: []
    logintime: []
    mschap: []
    ntlm_auth:
      disabled: true  # not configured by default
    pap: []
    passwd:  # passwd module allows authorization via passwd-like file.
      disabled: true  # defaults to /etc/passwd
    preprocess: []  # This module processes the 'huntgroups' and 'hints' files.
    radutmp: []  # Write a 'utmp' style file, of which users are currently logged in.
    realm: []  # Realm module, for proxying.
    replicate:  # Replicate packet(s) to a home server.
      disabled: true  # not configured by default
    soh: []  # implements support for Microsoft’s Statement of Health (SoH) protocol.
    sql:
      disabled: true  # not configured by default
      config_template: "modules/sql.j2"
      dialect: "mysql"
      server: []
      login: "radius"
      password: []
      radius_db: "radius"
      acct_table1: "radacct"
      acct_table2: "radacct"
      postauth_table: "radpostauth"
      authcheck_table: "radcheck"
      authreply_table: "radreply"
      groupcheck_table: "radgroupcheck"
      groupreply_table: "radgroupreply"
      usergroup_table: "radusergroup"
      deletestalesessions: yes
      client_table: "nas"
    sradutmp: []  # "Safe" radutmp - does not contain caller ID
    unix: []
    unpack: []
    utf8: []
```

Dependencies
------------

None

License
-------

GPL-3.0-or-later

Author Information
------------------

Cees Moerkerken