snmptt
=========

An Ansible role to manage [snmptt][snmptt].

Requirements
------------

This presently does not attempt to configure *snmpd* nor
*/etc/snmp/snmptrapd.conf*.  You will have to configure that separately
to feed traps to [snmptt][snmptt].

Here is an example configuration for *snmptrapd.conf*:

```
traphandle default /usr/sbin/snmptthandler
```

Role Variables
--------------

For details on configuring [snmptt][snmptt], refer to the
[documentation](http://www.snmptt.org/docs/snmptt.shtml).

- **snmptt_mode**: Whether to run as *standalone* or *daemon*.  The
  default is `daemon`.
- **snmptt_multiple_event**: Boolean for whether to allow multiple trap
  definitions to be executed for the same trap.  Defaults to `yes`.
- **snmptt_dns_enable**: Boolean for whether to enable DNS resolution of
  the IP address associated with the device that sent the trap.
  Defaults to `yes`.
- **snmptt_strip_domain**:  Determines whether and how to strip the
  domain from a FQDN.  Defaults to `0`.
- **snmptt_strip_domain_list**: List of domain names that should be
  stripped.  Defaults to empty list.
- **snmptt_resolve_value_ip_addresses**: Boolean for whether to resolve
  IP addresses in the VALUE of variable bindings.  Defaults to `no`.
- **snmptt_net_snmp_perl_enable**: Boolean for whether to enable the
  Perl module with *Net-SNMP*.  Defaults to `yes`.
- **snmptt_net_snmp_perl_cache_enable**: Boolean for whether to enable
  caching of OID and ENUM translations when using Perl with *Net-SNMP*.
  Defaults to `yes`.
- **snmptt_net_snmp_perl_best_guess**: Boolean for whether to use best
  guess parameter with *Net-SNMP* and Perl.  Defaults to `no`.
- **snmptt_translate_log_trap_oid**: Determines how to translate the
  trap OID for logging.  Defaults to `1`.
- **snmptt_translate_value_oids**: Determines how to translate OIDs in
  the value of a trap.  Defaults to `1`.
- **snmptt_translate_enterprise_oid_format**: Determines how the
  symbolic enterprise OID will be displayed.  Defaults to `1`.
- **snmptt_translate_trap_oid_format**: Determines how the symbolic trap
  OID will be displayed for *$0*.  Defaults to `1`.
- **snmptt_translate_varname_oid_format**: Determines how the symoblic
  trap OID will be displayed for *$v* and other variables.  Defaults to `1`.
- **snmptt_translate_integers**: Boolean for whether convert INTEGER
  values to enumeration tags as defined in the MIB files.  Defaults to `yes`.
- **snmptt_dynamic_nodes**: Boolean for whether to have NODES files
  loaded each time a trap is processed.  Defaults to `no`.
- **snmptt_description_mode**: Determines whether to use *$D*
  substitution variable to include the description text from
  *snmptt.conf* or MIB files.  Defaults to `0`.
- **snmptt_threads_enable**: Boolean for whether to use threads.
  Defaults to `no`.
- **snmptt_threads_max**: If using threads, the maximum number of
  threads that can execute at once.  Defaults to `10`.
- **snmptt_daemon_fork**: Boolean for whether to fork as a daemon.
  Defaults to `yes`.
- **snmptt_daemon_uid**: Username of the process owner after forking.
  Defaults to `snmptt`.
- **snmptt_spool_directory**: Path to spool directory.  Defaults to
  `/var/spool/snmptt/`.  [snmptt][snmptt] requires a trailing slash.
- **snmptt_sleep**: Time for daemon to sleep between runs processing the
  spool directory.  Defaults to `5`.
- **snmptt_use_trap_time**:  Boolean for whether to use trap time.
  Defaults to `yes`.
- **snmptt_stdout_enable**: Boolean for whether to enable logging to
  STDOUT.  Default is `no`.
- **snmptt_log_enable**: Boolean for whether to enable text logging of
  traps.  Default is `no`.
- **snmptt_log_file**: Path to file where text logging of traps should occur.
  Default is `/var/log/snmptt/snmptt.log`.
- **snmptt_log_system_enable**: Boolean for whether to enable system
  log.  Default is `no`.
- **snmptt_log_system_file**: Path to file where system logging should
  occur.  Default is `/var/log/snmptt/snmpttsystem.log`.
- **snmptt_unknown_trap_log_enable**: Boolean for whether to log unknown
  traps.  Default is `yes`.
- **snmptt_unknown_trap_log_file**: Path to file to log unknown traps.
  Default is `/var/log/snmptt/snmpttunknown.log`.
- **snmptt_statistics_interval**: Interval to log statistics.  Default
  is `0`.
- **snmptt_syslog_enable**: Boolean for whether to enable syslog.
  Default is `yes`.
- **snmptt_syslog_level**: Syslog level to use.  Default is `info`.
- **snmptt_syslog_facility**: Syslog facility to use.  Default is `daemon`.
- **snmptt_syslog_system_enable**: Boolean for whether to enable system
  logging to syslog.  Default is `yes`.
- **snmptt_syslog_system_level**: Syslog level to use for system
  logging.  Default is `info`.
- **snmptt_syslog_system_facility**: Syslog facility to use for system
  logging.  Default is `daemon`.
- **snmptt_exec_enable**: Boolean for whether to enable EXEC
  definitions.  Defaults to `yes`.
- **snmptt_pre_exec_enable**: Boolean for whether to enable PREEXEC
  definitions.  Defaults to `yes`.
- **snmptt_exec_escape**: Boolean for whether to escape wildcards in
  EXEC and PREEXEC definitions.  Defaults to `yes`.
- **snmptt_debugging_file**: Path to debugging output file.  Defaults to
  `/var/log/snmptt/snmptt.debug`.
- **snmptt_debugging_file_handler**: Path to debugging file handler.
  Defaults to `/var/log/snmptt/snmptthandler.debug`.
- **snmptt_trap_file**: Path to the SNMP trap file.  Defaults to
  `/etc/snmp/snmptt.conf`.
- **snmp_trap_definitions**: A list of *snmptt* trap definitions that is
  used to template the file *snmptt.conf*.  The default includes
  defintions for *coldStart*, *warmStart*, *linkDown*, *linkUp*, and
  *authenticationFailure*.  You will have to specify the *snmptt* trap
  syntax directly.  Here is an example:
```
  EVENT warmStart .1.3.6.1.6.3.1.1.5.2 "Status Events" Normal
  FORMAT Device reinitialized (warmStart)
  SDESC
  A warmStart trap signifies that the SNMPv2 entity, acting
  in an agent role, is reinitializing itself such that its
  configuration is unaltered.
  EDESC
```
  

Dependencies
------------

No dependency on other roles.

Example Playbook
----------------

A trivial example:

    - hosts: servers
      roles:
      - { role: sfromm.snmptt }


License
-------

GPLv2

Author Information
------------------

See https://github.com/sfromm

[snmptt]: http://www.snmptt.org/
