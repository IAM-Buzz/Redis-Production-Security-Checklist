# Redis Production Security Checklist

## Architecture

### Standalone and Cluster Mode

1. Ensure Redis is always deployed inside a trusted network.
2. Ensure protected mode is on unless ACLs or AUTH is enabled.
3. Ensure the Redis Log file is configured.
4. Ensure Redis is run as a non-privileged user.
5. Ensure Redis files are given a non-privileged group
6. Ensure Redis logs, files and configurations are not readable or writable by others on the operating system.
7. Ensure the Redis Log file is rotated.
8. Ensure Redis configuration files are not accessible by others, such as `740` permissions.
9. Ensure you leverage the latest Redis client and server version.
10. Consider IP restrictions through the network or operating system to ensure only trusted IPs can connect to Redis.
11. Consider using client side encryption to encrypt sensitive data.
12. Consider if TLS is right for your use case.
13. Consider changing the default Redis port
14. Consider backing up RDB and AOF files to a remote external location.
15. Ensure you select the right persistence method for your use case.
16. Consider sending Redis log files to syslog.

### Cluster Mode Only

1. Ensure that an odd number of at least 3 nodes are deployed in the cluster
2. Ensure any reboot schedules do not reboot enough nodes at the same time to lose quorum.

## Account Management

### Standalone and Cluster Mode

1. Ensure AUTH or ACLs are enabled.
2. Ensure all users have a strong password.
3. Ensure the default user is disabled, unless required for backwards compatibility.
4. Ensure the `@dangerous` command category is excluded from all users and dangerous commands are given on a case by case basis.
5. Ensure that an external ACL file is used to configure ACLs.
6. Ensure that users configured in an external ACL file or the `redis.conf` file store passwords in hashed format.
7. Ensure that the `requirepass` is only set if backwards compatibility is required.
8. Consider if all ACL users are configured to least privilege.
9. Consider renaming commands to disable them entirely

### Cluster Mode Only

1. Ensure that `masteruser` is used for authentication to masters.
2. Ensure that sentinel `auth-user` is used if you are using sentinel.

## Transport layer Security

### Standalone & Cluster Mode

1. Ensure non-TLS ports are disabled.
2. Ensure strong cipher suites are used with Redis.
3. Ensure appropriate modern TLS protocols are used.
4. Ensure client authentication is used.
5. Ensure server ciphers are prefered.
6. Ensure TLS is configured for replication
7. Ensure key files are given `400` permissions.
8. Ensure key files are owned by the Redis user.

### Cluster Mode Only

1. Ensure TLS is enabled on the cluster bus
