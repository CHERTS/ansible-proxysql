# ProxySQL Ansible role

This role will install proxysql on RedHat/CentOS (7, 8) and Ubuntu (16.04, 18.04, 20.04) from [sysown release](https://github.com/sysown/proxysql/releases).

## Requirements

Tested on 2.5.0. Should work on 2.3+

## Role Handlers

| Name                     | Type    | Description                                                                 |
| ------------------------ | ------- | --------------------------------------------------------------------------- |
| Restart proxysql normal  | service | Restarts proxysql using service (SysV based) when proxysql_initial is False |
| Restart proxysql initial | command | Restarts proxysql in initial mode when proxysql_initial is True             |
| Restart proxysql         | Virtual | Calls all above handlers                                                    |

## Tags

| Name     | Description           |
| -------- | --------------------- |
| proxysql | Applies to whole role |


## Role Variables

ProxySQL global variables:

| Name                       | Default   | Type   | Description                                                       |
| -----                      | -------   | ------ | -----------                                                       |
| proxysql_datadir           | /var/lib/proxysql | String | Default ProxySQL data directory                           |
| proxysql_errorlog          | /var/lib/proxysql/proxysql.log | String | Default ProxySQL log file name               |

ProxySQL admin variables, [see detail docs](https://proxysql.com/documentation/global-variables/admin-variables/):

| Name                       | Default   | Type   | Description                                                       |
| -----                      | -------   | ------ | -----------                                                       |
| proxysql_admin_user        | admin     | String | Username for ProxySQL admin                                       |
| proxysql_admin_password    | admin     | String | Password for the above user                                       |
| proxysql_admin_interface   | 127.0.0.1 | String | Bind address for admin interface                                  |
| proxysql_admin_port        | 6032      | Number | Bind port for administrative interface                            |
| proxysql_admin_socket      | /tmp/proxysql_admin.sock | String | ProxySQL admin socket path                         |
| proxysql_web_enabled       | True      | Bool   | Enable Web interface, use https://x.x.x.x:6080                    |
| proxysql_web_port          | 6080      | Number | Bind port for Web interface                                       |
| proxysql_refresh_interval  | 2000      | Number | Refresh interval, see doc [admin-refresh_interval](https://proxysql.com/documentation/global-variables/admin-variables/#admin-refresh_interval) |
| proxysql_stats_user        | stats     | String | admin-stats_credentials user name                                 |
| proxysql_stats_password    | admin     | String | admin-stats_credentials user password                             |
| proxysql_admin_raw_options |           | Array  | Other admin options                                               |
| proxysql_initial           | False     | Bool   | Wipes existing config database when True (see --initial CLI flag) |
| proxysql_mysql_interface   | 127.0.0.1 | String | MySQL bind interface                                              |
| proxysql_mysql_port        | 6033      | Number | MySQL bind port                                                   |

ProxySQL mysql variables, [see detail docs](https://proxysql.com/documentation/global-variables/mysql-variables/):

| Name                                            | Default   | Type   | Description                                                       |
| -----                                           | -------   | ------ | -----------                                                       |
| proxysql_mysql_interface                        | 0.0.0.0   | String | Interfaces for incoming MySQL traffic                             |
| proxysql_mysql_port                             | 6033      | Number | Port for incoming MySQL traffic                                   | 
| proxysql_mysql_socket                           | /tmp/proxysql.sock | String | UNIX domain sockets                                      |
| proxysql_threads                                | 4         | Number | The number of background threads that ProxySQL uses in order to process MySQL traffic | 
| proxysql_max_connections                        | 2048      | Number | The maximum number of client connections that the proxy can handle | 
| proxysql_default_query_delay                    | 0         | Number | This variable allows to create a simple throttling mechanism, delaying the excution of queries to the backends | 
| proxysql_default_query_timeout                  | 86400000  | Number | ProxySQL is able to track the execution time of every query that has sent to the backend, and is able to timeout such queries if they run for too long | 
| proxysql_have_compress                          | True      | Bool   | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_poll_timeout                           | 2000      | Number | The minimal timeout used by the proxy in order to detect incoming/outgoing traffic via the poll() system call | 
| proxysql_default_schema                         | information_schema | String | The default schema to be used for incoming MySQL client connections which do not specify a schema name |
| proxysql_stacksize                              | 1048576   | Number | The stack size to be used with the background threads that the proxy uses to handle MySQL traffic and connect to the backends | 
| proxysql_server_capabilities                    | 569867    | Number | The bitmask of MySQL capabilities (encoded as bits) with which the proxy will respond to clients connecting to it | 
| proxysql_server_version                         | 5.5.30    | String | The server version with which the proxy will respond to the clients | 
| proxysql_connect_timeout_server                 | 1000      | Number | The timeout for a single attempt at connecting to a backend server from proxysql | 
| proxysql_monitor_user                           | monitor   | String | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_monitor_password                       | monitor   | String | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_monitor_history                        | 600000    | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_monitor_connect_interval               | 60000     | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_monitor_ping_interval                  | 10000     | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_monitor_read_only_interval             | 1500      | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_monitor_read_only_timeout              | 500       | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_monitor_slave_lag_when_null            | 60        | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_monitor_replication_lag_interval       | 10000     | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_ping_timeout_server                    | 500       | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_ping_interval_server_msec              | 120000    | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_commands_stats                         | True      | Bool   | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_sessions_sort                          | True      | Bool   | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_connect_retries_on_failure             | 10        | Number | [See docs](https://proxysql.com/documentation/global-variables/mysql-variables/) | 
| proxysql_mysql_raw_options                      | long_query_time=3  | Array | Other mysql variable options |

Query rules, servers and users:

| Name                                   | Default   | Type   | Description                                                       |
| -----                                  | -------   | ------ | -----------                                                       |
| proxysql_mysql_query_rules             | []        | Array  | Configuration-file query rules                                    |
| proxysql_mysql_servers                 | []        | Array  | Configuration-file servers                                        |
| proxysql_mysql_users                   | []        | Array  | Configuration-file users                                          |
| proxysql_mysql_replication_hostgroups  | []        | Array  | Configuration-file replication hostgroups                         |

If you don't want to list `proxy_mysql_servers` in variables, you can set `proxy_mysql_servers_group` instead.
The rolle will populate mysql_servers from the group name.

However, in this case, be sure to set the following variables for _eachserver_ in the group:

| Name                              | Default | Type   | Description                                         |
| -----                             | ------- | ------ | --------------------------------------------        |
| proxysql_upstream_mysql_interface | false   | String | Interface **name** upstream MySQL server listens on |
| proxysql_upstream_mysql_port      | 3306    | String | Port upstream MySQL listens on                     |
| proxysql_hostgroup                | false   | Number | Hostgroup this MySQL server belongs to              |

Note that you can not use both `proxy_mysql_servers_group` and `proxy_mysql_servers` at the same time !

When using cluster mode, the following variables must be set:

| Name                           | Default | Type   | Description                                       |
| -----                          | ------- | ------ | --------------------------------------------      |
| proxysql_cluster_name          | false   | String | ProxySQL name                                     |
| proxysql_cluster_password      | false   | String | ProxySQL password for cluster communications      |
| proxysql_cluster_servers_group | false   | String | Ansible group containing ProxySQL cluster members |

## Example

### Requirements

```yaml
- src: git+ssh://git@github.com/cherts/ansible-proxysql.git
  version: origin/main
```
_Use a fixed tag instead of origin/master if possible_

### Playbook

```yaml
- hosts: proxylb
  roles:
    - proxysql
```

### Inventory

```yaml
proxysql_mysql_query_rules:
  - match_pattern: "^SELECT .* FOR UPDATE$"
    destination_hostgroup: 0
  - match_pattern: "^SELECT"
    destination_hostgroup: 1

proxysql_mysql_servers:
   - address: 1.2.3.4
     port: 3306
     hostgroup: 0
   - address: 5.6.7.8
     port: 3306
     hostgroup: 1
```

## Notes

This role follows [Semantic Versionning](http://semver.org/) conventions.

Besides proxysql, the `mysql-common` package will be installed by this role.

# License

MIT

# Author Information

This role is based on the role [ansible-proxysql from @leucos](https://github.com/leucos/ansible-proxysql) and is modified by me (Mikhail Grigorev).

Please send suggestion or pull requests to make this role better. Also let me know if you encounter any issues installing or using this role.

Github: https://github.com/CHERTS/ansible-proxysql

mail: sleuthhound [ at ] gmail . com
