Title: PostgreSQL: Documentation: 18: Part III. Server Administration
Mapped Topic: Relational database foundations
Source URL: https://www.postgresql.org/docs/current/admin.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:32+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

February 26, 2026: [
PostgreSQL 18.3, 17.9, 16.13, 15.17, and 14.22 Released!
](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/)

Development Versions:
[devel](https://www.postgresql.org/docs/devel/admin.html)

This part covers topics that are of interest to a PostgreSQL administrator. This includes installation, configuration of the server, management of users and databases, and maintenance tasks. Anyone running PostgreSQL server, even for personal use, but especially in production, should be familiar with these topics.

The information attempts to be in the order in which a new user should read it. The chapters are self-contained and can be read individually as desired. The information is presented in a narrative form in topical units. Readers looking for a complete description of a command are encouraged to review the [Part VI](https://www.postgresql.org/reference.html).

The first few chapters are written so they can be understood without prerequisite knowledge, so new users who need to set up their own server can begin their exploration. The rest of this part is about tuning and management; that material assumes that the reader is familiar with the general use of the PostgreSQL database system. Readers are encouraged review the [Part I](https://www.postgresql.org/tutorial.html) and [Part II](https://www.postgresql.org/sql.html) parts for additional information.

**Table of Contents**

[16. Installation from Binaries](https://www.postgresql.org/install-binaries.html)[17. Installation from Source Code](https://www.postgresql.org/installation.html)[18. Server Setup and Operation](https://www.postgresql.org/runtime.html)-
[18.1. The PostgreSQL User Account](https://www.postgresql.org/postgres-user.html)[18.2. Creating a Database Cluster](https://www.postgresql.org/creating-cluster.html)[18.3. Starting the Database Server](https://www.postgresql.org/server-start.html)[18.4. Managing Kernel Resources](https://www.postgresql.org/kernel-resources.html)[18.5. Shutting Down the Server](https://www.postgresql.org/server-shutdown.html)[18.6. Upgrading a PostgreSQL Cluster](https://www.postgresql.org/upgrading.html)[18.7. Preventing Server Spoofing](https://www.postgresql.org/preventing-server-spoofing.html)[18.8. Encryption Options](https://www.postgresql.org/encryption-options.html)[18.9. Secure TCP/IP Connections with SSL](https://www.postgresql.org/ssl-tcp.html)[18.10. Secure TCP/IP Connections with GSSAPI Encryption](https://www.postgresql.org/gssapi-enc.html)[18.11. Secure TCP/IP Connections with SSH Tunnels](https://www.postgresql.org/ssh-tunnels.html)[18.12. Registering Event Log on Windows](https://www.postgresql.org/event-log-registration.html)

[19. Server Configuration](https://www.postgresql.org/runtime-config.html)-
[19.1. Setting Parameters](https://www.postgresql.org/config-setting.html)[19.2. File Locations](https://www.postgresql.org/runtime-config-file-locations.html)[19.3. Connections and Authentication](https://www.postgresql.org/runtime-config-connection.html)[19.4. Resource Consumption](https://www.postgresql.org/runtime-config-resource.html)[19.5. Write Ahead Log](https://www.postgresql.org/runtime-config-wal.html)[19.6. Replication](https://www.postgresql.org/runtime-config-replication.html)[19.7. Query Planning](https://www.postgresql.org/runtime-config-query.html)[19.8. Error Reporting and Logging](https://www.postgresql.org/runtime-config-logging.html)[19.9. Run-time Statistics](https://www.postgresql.org/runtime-config-statistics.html)[19.10. Vacuuming](https://www.postgresql.org/runtime-config-vacuum.html)[19.11. Client Connection Defaults](https://www.postgresql.org/runtime-config-client.html)[19.12. Lock Management](https://www.postgresql.org/runtime-config-locks.html)[19.13. Version and Platform Compatibility](https://www.postgresql.org/runtime-config-compatible.html)[19.14. Error Handling](https://www.postgresql.org/runtime-config-error-handling.html)[19.15. Preset Options](https://www.postgresql.org/runtime-config-preset.html)[19.16. Customized Options](https://www.postgresql.org/runtime-config-custom.html)[19.17. Developer Options](https://www.postgresql.org/runtime-config-developer.html)[19.18. Short Options](https://www.postgresql.org/runtime-config-short.html)

[20. Client Authentication](https://www.postgresql.org/client-authentication.html)-
[20.1. The](https://www.postgresql.org/auth-pg-hba-conf.html)`pg_hba.conf`

File[20.2. User Name Maps](https://www.postgresql.org/auth-username-maps.html)[20.3. Authentication Methods](https://www.postgresql.org/auth-methods.html)[20.4. Trust Authentication](https://www.postgresql.org/auth-trust.html)[20.5. Password Authentication](https://www.postgresql.org/auth-password.html)[20.6. GSSAPI Authentication](https://www.postgresql.org/gssapi-auth.html)[20.7. SSPI Authentication](https://www.postgresql.org/sspi-auth.html)[20.8. Ident Authentication](https://www.postgresql.org/auth-ident.html)[20.9. Peer Authentication](https://www.postgresql.org/auth-peer.html)[20.10. LDAP Authentication](https://www.postgresql.org/auth-ldap.html)[20.11. RADIUS Authentication](https://www.postgresql.org/auth-radius.html)[20.12. Certificate Authentication](https://www.postgresql.org/auth-cert.html)[20.13. PAM Authentication](https://www.postgresql.org/auth-pam.html)[20.14. BSD Authentication](https://www.postgresql.org/auth-bsd.html)[20.15. OAuth Authorization/Authentication](https://www.postgresql.org/auth-oauth.html)[20.16. Authentication Problems](https://www.postgresql.org/client-authentication-problems.html)

[21. Database Roles](https://www.postgresql.org/user-manag.html)[22. Managing Databases](https://www.postgresql.org/managing-databases.html)[23. Localization](https://www.postgresql.org/charset.html)[24. Routine Database Maintenance Tasks](https://www.postgresql.org/maintenance.html)[25. Backup and Restore](https://www.postgresql.org/backup.html)[26. High Availability, Load Balancing, and Replication](https://www.postgresql.org/high-availability.html)[27. Monitoring Database Activity](https://www.postgresql.org/monitoring.html)[28. Reliability and the Write-Ahead Log](https://www.postgresql.org/wal.html)[29. Logical Replication](https://www.postgresql.org/logical-replication.html)[30. Just-in-Time Compilation (JIT)](https://www.postgresql.org/jit.html)[31. Regression Tests](https://www.postgresql.org/regress.html)

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use
[this form](https://www.postgresql.org/account/comments/new/18/admin.html/)
to report a documentation issue.
