------
####  Greenplum SQL Statement
##### A. `Kill Processes`
- <b>Step 1 ： Show All Running Processes</b>

```SQL
SELECT		*
FROM 		pg_stat_activity;
```
- <b>Step 2 ： Kill procpid </b>

```SQL
SELECT		pg_cancel_backend( [the process number found in step1] ) ;
```
> Reference : https://discuss.pivotal.io/hc/en-us/articles/202032703-How-to-cancel-running-queries-OR-idle-sessions-

<br>

##### B. `Check Table Size`

```SQL
SELECT		relname as "Table",
		pg_size_pretty(pg_total_relation_size(relid)) As "Size",
		pg_size_pretty(pg_total_relation_size(relid) - pg_relation_size(relid)) as "External Size"
FROM 		pg_catalog.pg_statio_user_tables 
WHERE		schemaname=' [schema name] '
```
