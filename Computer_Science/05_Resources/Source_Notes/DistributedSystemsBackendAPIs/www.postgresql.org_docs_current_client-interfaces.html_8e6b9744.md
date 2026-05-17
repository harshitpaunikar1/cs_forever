Title: PostgreSQL: Documentation: 18: Part IV. Client Interfaces
Mapped Topic: Relational database foundations
Source URL: https://www.postgresql.org/docs/current/client-interfaces.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:33+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

February 26, 2026: [
PostgreSQL 18.3, 17.9, 16.13, 15.17, and 14.22 Released!
](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/)

Development Versions:
[devel](https://www.postgresql.org/docs/devel/client-interfaces.html)

This part describes the client programming interfaces distributed with PostgreSQL. Each of these chapters can be read independently. There are many external programming interfaces for client programs that are distributed separately. They contain their own documentation ([Appendix H](https://www.postgresql.org/external-projects.html) lists some of the more popular ones). Readers of this part should be familiar with using SQL to manipulate and query the database (see [Part II](https://www.postgresql.org/sql.html)) and of course with the programming language of their choice.

**Table of Contents**

[32. libpq — C Library](https://www.postgresql.org/libpq.html)-
[32.1. Database Connection Control Functions](https://www.postgresql.org/libpq-connect.html)[32.2. Connection Status Functions](https://www.postgresql.org/libpq-status.html)[32.3. Command Execution Functions](https://www.postgresql.org/libpq-exec.html)[32.4. Asynchronous Command Processing](https://www.postgresql.org/libpq-async.html)[32.5. Pipeline Mode](https://www.postgresql.org/libpq-pipeline-mode.html)[32.6. Retrieving Query Results in Chunks](https://www.postgresql.org/libpq-single-row-mode.html)[32.7. Canceling Queries in Progress](https://www.postgresql.org/libpq-cancel.html)[32.8. The Fast-Path Interface](https://www.postgresql.org/libpq-fastpath.html)[32.9. Asynchronous Notification](https://www.postgresql.org/libpq-notify.html)[32.10. Functions Associated with the](https://www.postgresql.org/libpq-copy.html)`COPY`

Command[32.11. Control Functions](https://www.postgresql.org/libpq-control.html)[32.12. Miscellaneous Functions](https://www.postgresql.org/libpq-misc.html)[32.13. Notice Processing](https://www.postgresql.org/libpq-notice-processing.html)[32.14. Event System](https://www.postgresql.org/libpq-events.html)[32.15. Environment Variables](https://www.postgresql.org/libpq-envars.html)[32.16. The Password File](https://www.postgresql.org/libpq-pgpass.html)[32.17. The Connection Service File](https://www.postgresql.org/libpq-pgservice.html)[32.18. LDAP Lookup of Connection Parameters](https://www.postgresql.org/libpq-ldap.html)[32.19. SSL Support](https://www.postgresql.org/libpq-ssl.html)[32.20. OAuth Support](https://www.postgresql.org/libpq-oauth.html)[32.21. Behavior in Threaded Programs](https://www.postgresql.org/libpq-threading.html)[32.22. Building libpq Programs](https://www.postgresql.org/libpq-build.html)[32.23. Example Programs](https://www.postgresql.org/libpq-example.html)

[33. Large Objects](https://www.postgresql.org/largeobjects.html)[34. ECPG — Embedded SQL in C](https://www.postgresql.org/ecpg.html)-
[34.1. The Concept](https://www.postgresql.org/ecpg-concept.html)[34.2. Managing Database Connections](https://www.postgresql.org/ecpg-connect.html)[34.3. Running SQL Commands](https://www.postgresql.org/ecpg-commands.html)[34.4. Using Host Variables](https://www.postgresql.org/ecpg-variables.html)[34.5. Dynamic SQL](https://www.postgresql.org/ecpg-dynamic.html)[34.6. pgtypes Library](https://www.postgresql.org/ecpg-pgtypes.html)[34.7. Using Descriptor Areas](https://www.postgresql.org/ecpg-descriptors.html)[34.8. Error Handling](https://www.postgresql.org/ecpg-errors.html)[34.9. Preprocessor Directives](https://www.postgresql.org/ecpg-preproc.html)[34.10. Processing Embedded SQL Programs](https://www.postgresql.org/ecpg-process.html)[34.11. Library Functions](https://www.postgresql.org/ecpg-library.html)[34.12. Large Objects](https://www.postgresql.org/ecpg-lo.html)[34.13. C++ Applications](https://www.postgresql.org/ecpg-cpp.html)[34.14. Embedded SQL Commands](https://www.postgresql.org/ecpg-sql-commands.html)[34.15. Informix Compatibility Mode](https://www.postgresql.org/ecpg-informix-compat.html)[34.16. Oracle Compatibility Mode](https://www.postgresql.org/ecpg-oracle-compat.html)[34.17. Internals](https://www.postgresql.org/ecpg-develop.html)

[35. The Information Schema](https://www.postgresql.org/information-schema.html)-
[35.1. The Schema](https://www.postgresql.org/infoschema-schema.html)[35.2. Data Types](https://www.postgresql.org/infoschema-datatypes.html)[35.3.](https://www.postgresql.org/infoschema-information-schema-catalog-name.html)`information_schema_catalog_name`

[35.4.](https://www.postgresql.org/infoschema-administrable-role-authorizations.html)`administrable_role_authorizations`

[35.5.](https://www.postgresql.org/infoschema-applicable-roles.html)`applicable_roles`

[35.6.](https://www.postgresql.org/infoschema-attributes.html)`attributes`

[35.7.](https://www.postgresql.org/infoschema-character-sets.html)`character_sets`

[35.8.](https://www.postgresql.org/infoschema-check-constraint-routine-usage.html)`check_constraint_routine_usage`

[35.9.](https://www.postgresql.org/infoschema-check-constraints.html)`check_constraints`

[35.10.](https://www.postgresql.org/infoschema-collations.html)`collations`

[35.11.](https://www.postgresql.org/infoschema-collation-character-set-applicab.html)`collation_character_set_applicability`

[35.12.](https://www.postgresql.org/infoschema-column-column-usage.html)`column_column_usage`

[35.13.](https://www.postgresql.org/infoschema-column-domain-usage.html)`column_domain_usage`

[35.14.](https://www.postgresql.org/infoschema-column-options.html)`column_options`

[35.15.](https://www.postgresql.org/infoschema-column-privileges.html)`column_privileges`

[35.16.](https://www.postgresql.org/infoschema-column-udt-usage.html)`column_udt_usage`

[35.17.](https://www.postgresql.org/infoschema-columns.html)`columns`

[35.18.](https://www.postgresql.org/infoschema-constraint-column-usage.html)`constraint_column_usage`

[35.19.](https://www.postgresql.org/infoschema-constraint-table-usage.html)`constraint_table_usage`

[35.20.](https://www.postgresql.org/infoschema-data-type-privileges.html)`data_type_privileges`

[35.21.](https://www.postgresql.org/infoschema-domain-constraints.html)`domain_constraints`

[35.22.](https://www.postgresql.org/infoschema-domain-udt-usage.html)`domain_udt_usage`

[35.23.](https://www.postgresql.org/infoschema-domains.html)`domains`

[35.24.](https://www.postgresql.org/infoschema-element-types.html)`element_types`

[35.25.](https://www.postgresql.org/infoschema-enabled-roles.html)`enabled_roles`

[35.26.](https://www.postgresql.org/infoschema-foreign-data-wrapper-options.html)`foreign_data_wrapper_options`

[35.27.](https://www.postgresql.org/infoschema-foreign-data-wrappers.html)`foreign_data_wrappers`

[35.28.](https://www.postgresql.org/infoschema-foreign-server-options.html)`foreign_server_options`

[35.29.](https://www.postgresql.org/infoschema-foreign-servers.html)`foreign_servers`

[35.30.](https://www.postgresql.org/infoschema-foreign-table-options.html)`foreign_table_options`

[35.31.](https://www.postgresql.org/infoschema-foreign-tables.html)`foreign_tables`

[35.32.](https://www.postgresql.org/infoschema-key-column-usage.html)`key_column_usage`

[35.33.](https://www.postgresql.org/infoschema-parameters.html)`parameters`

[35.34.](https://www.postgresql.org/infoschema-referential-constraints.html)`referential_constraints`

[35.35.](https://www.postgresql.org/infoschema-role-column-grants.html)`role_column_grants`

[35.36.](https://www.postgresql.org/infoschema-role-routine-grants.html)`role_routine_grants`

[35.37.](https://www.postgresql.org/infoschema-role-table-grants.html)`role_table_grants`

[35.38.](https://www.postgresql.org/infoschema-role-udt-grants.html)`role_udt_grants`

[35.39.](https://www.postgresql.org/infoschema-role-usage-grants.html)`role_usage_grants`

[35.40.](https://www.postgresql.org/infoschema-routine-column-usage.html)`routine_column_usage`

[35.41.](https://www.postgresql.org/infoschema-routine-privileges.html)`routine_privileges`

[35.42.](https://www.postgresql.org/infoschema-routine-routine-usage.html)`routine_routine_usage`

[35.43.](https://www.postgresql.org/infoschema-routine-sequence-usage.html)`routine_sequence_usage`

[35.44.](https://www.postgresql.org/infoschema-routine-table-usage.html)`routine_table_usage`

[35.45.](https://www.postgresql.org/infoschema-routines.html)`routines`

[35.46.](https://www.postgresql.org/infoschema-schemata.html)`schemata`

[35.47.](https://www.postgresql.org/infoschema-sequences.html)`sequences`

[35.48.](https://www.postgresql.org/infoschema-sql-features.html)`sql_features`

[35.49.](https://www.postgresql.org/infoschema-sql-implementation-info.html)`sql_implementation_info`

[35.50.](https://www.postgresql.org/infoschema-sql-parts.html)`sql_parts`

[35.51.](https://www.postgresql.org/infoschema-sql-sizing.html)`sql_sizing`

[35.52.](https://www.postgresql.org/infoschema-table-constraints.html)`table_constraints`

[35.53.](https://www.postgresql.org/infoschema-table-privileges.html)`table_privileges`

[35.54.](https://www.postgresql.org/infoschema-tables.html)`tables`

[35.55.](https://www.postgresql.org/infoschema-transforms.html)`transforms`

[35.56.](https://www.postgresql.org/infoschema-triggered-update-columns.html)`triggered_update_columns`

[35.57.](https://www.postgresql.org/infoschema-triggers.html)`triggers`

[35.58.](https://www.postgresql.org/infoschema-udt-privileges.html)`udt_privileges`

[35.59.](https://www.postgresql.org/infoschema-usage-privileges.html)`usage_privileges`

[35.60.](https://www.postgresql.org/infoschema-user-defined-types.html)`user_defined_types`

[35.61.](https://www.postgresql.org/infoschema-user-mapping-options.html)`user_mapping_options`

[35.62.](https://www.postgresql.org/infoschema-user-mappings.html)`user_mappings`

[35.63.](https://www.postgresql.org/infoschema-view-column-usage.html)`view_column_usage`

[35.64.](https://www.postgresql.org/infoschema-view-routine-usage.html)`view_routine_usage`

[35.65.](https://www.postgresql.org/infoschema-view-table-usage.html)`view_table_usage`

[35.66.](https://www.postgresql.org/infoschema-views.html)`views`

[this form](https://www.postgresql.org/account/comments/new/18/client-interfaces.html/)
to report a documentation issue.
