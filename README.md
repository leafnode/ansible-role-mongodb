# mongodb

[![Build Status](https://travis-ci.com/iroquoisorg/ansible-role-mongodb.svg?branch=master)](https://travis-ci.com/iroquoisorg/ansible-role-memcached)

Ansible role for mongodb

This role was prepared and tested for Ubuntu 16.04.

# Installation

`$ ansible-galaxy install iroquoisorg.mongodb`

# Default settings

```


mongodb_package: mongodb-org
mongodb_version: "4.0"
mongodb_apt_keyserver: keyserver.ubuntu.com
mongodb_pymongo_from_pip: true                   # Install latest PyMongo via PIP or package manager

mongodb_force_wait_for_port: false
mongodb_user_update_password: "on_create"        # MongoDB user password update default policy
mongodb_manage_service: true

mongodb_user: mongodb
mongodb_uid:
mongodb_gid:
mongodb_daemon_name: "{{ 'mongod' if ('mongodb-org' in mongodb_package) else 'mongodb' }}"

## net Options
mongodb_net_bindip: 127.0.0.1                    # Comma separated list of ip addresses to listen on
mongodb_net_http_enabled: false                  # Enable http interface
mongodb_net_ipv6: false                          # Enable IPv6 support (disabled by default)
mongodb_net_maxconns: 65536                      # Max number of simultaneous connections
mongodb_net_port: 27017                          # Specify port number

## processManagement Options
mongodb_processmanagement_fork: false            # Fork server process

## security Options
# Disable or enable security. Possible values: 'disabled', 'enabled'
mongodb_security_authorization: "disabled"
mongodb_security_keyfile: /etc/mongodb-keyfile   # Specify path to keyfile with password for inter-process authentication

## storage Options
mongodb_storage_dbpath: /data/db                 # Directory for datafiles
# The storage engine for the mongod database. Available values:
# 'mmapv1', 'wiredTiger'
mongodb_storage_engine: "{{ 'mmapv1' if mongodb_version[0:3] == '3.0' else 'wiredTiger' }}"
# mmapv1 specific options
mongodb_storage_quota_enforced: false            # Limits each database to a certain number of files
mongodb_storage_quota_maxfiles: 8                # Number of quota files per DB
mongodb_storage_smallfiles: false                # Very useful for non-data nodes

mongodb_storage_journal_enabled: true            # Enable journaling
mongodb_storage_prealloc: true                   # Enable data file preallocation

## systemLog Options
## The destination to which MongoDB sends all log output. Specify either 'file' or 'syslog'.
## If you specify 'file', you must also specify mongodb_systemlog_path.
mongodb_systemlog_destination: "file"
mongodb_systemlog_logappend: true                                        # Append to logpath instead of over-writing
mongodb_systemlog_path: /var/log/mongodb/{{ mongodb_daemon_name }}.log   # Log file to send write to instead of stdout

## replication Options
mongodb_replication_replset:                      # Enable replication <setname>[/<optionalseedhostlist>]
mongodb_replication_replindexprefetch: "all"      # specify index prefetching behavior (if secondary) [none|_id_only|all]
mongodb_replication_oplogsize: 1024               # specifies a maximum size in megabytes for the replication operation log

# MMS Agent
mongodb_mms_agent_pkg: https://mms.mongodb.com/download/agent/automation/mongodb-mms-automation-agent-manager_1.4.2.783-1_amd64.deb
mongodb_mms_group_id: ""
mongodb_mms_api_key: ""
mongodb_mms_base_url: https://mms.mongodb.com

# password for inter-process authentication
# please regenerate this file on production environment with command 'openssl rand -base64 741'
mongodb_keyfile_content: |
  8pYcxvCqoe89kcp33KuTtKVf5MoHGEFjTnudrq5BosvWRoIxLowmdjrmUpVfAivh
  CHjqM6w0zVBytAxH1lW+7teMYe6eDn2S/O/1YlRRiW57bWU3zjliW3VdguJar5i9
  Z+1a8lI+0S9pWynbv9+Ao0aXFjSJYVxAm/w7DJbVRGcPhsPmExiSBDw8szfQ8PAU
  2hwRl7nqPZZMMR+uQThg/zV9rOzHJmkqZtsO4UJSilG9euLCYrzW2hdoPuCrEDhu
  Vsi5+nwAgYR9dP2oWkmGN1dwRe0ixSIM2UzFgpaXZaMOG6VztmFrlVXh8oFDRGM0
  cGrFHcnGF7oUGfWnI2Cekngk64dHA2qD7WxXPbQ/svn9EfTY5aPw5lXzKA87Ds8p
  KHVFUYvmA6wVsxb/riGLwc+XZlb6M9gqHn1XSpsnYRjF6UzfRcRR2WyCxLZELaqu
  iKxLKB5FYqMBH7Sqg3qBCtE53vZ7T1nefq5RFzmykviYP63Uhu/A2EQatrMnaFPl
  TTG5CaPjob45CBSyMrheYRWKqxdWN93BTgiTW7p0U6RB0/OCUbsVX6IG3I9N8Uqt
  l8Kc+7aOmtUqFkwo8w30prIOjStMrokxNsuK9KTUiPu2cj7gwYQ574vV3hQvQPAr
  hhb9ohKr0zoPQt31iTj0FDkJzPepeuzqeq8F51HB56RZKpXdRTfY8G6OaOT68cV5
  vP1O6T/okFKrl41FQ3CyYN5eRHyRTK99zTytrjoP2EbtIZ18z+bg/angRHYNzbgk
  lc3jpiGzs1ZWHD0nxOmHCMhU4usEcFbV6FlOxzlwrsEhHkeiununlCsNHatiDgzp
  ZWLnP/mXKV992/Jhu0Z577DHlh+3JIYx0PceB9yzACJ8MNARHF7QpBkhtuGMGZpF
  T+c73exupZFxItXs1Bnhe3djgE3MKKyYvxNUIbcTJoe7nhVMrwO/7lBSpVLvC4p3
  wR700U0LDaGGQpslGtiE56SemgoP

# names and passwords for administrative users
mongodb_user_admin_name: siteUserAdmin
mongodb_user_admin_password: passw0rd

mongodb_root_admin_name: siteRootAdmin
mongodb_root_admin_password: passw0rd

mongodb_root_backup_name: "backupuser"
mongodb_root_backup_password: "passw0rd"

```
