# Performance

## Odoo configuration

Get CPU cores:

    nproc --all

```
workers = (CPU cores * 2 + 1)
limit_memory_soft = (671088640 x workers)
limit_memory_hard = (805306368 x workers)
limit_request = 8192
limit_time_cpu = 60
limit_time_real = 120
max_cron_threads = 2
```

## Postgres configuration

**postgresql.conf**
```
shared_buffers = (20% of the available memory in MB)
effective_cache_size = (50% of the available memory in MB)
shared_preload_libraries = 'pg_stat_statements'
track_activity_query_size = 2048
pg_stat_statements.max = 1000
pg_stat_statements.track = all
log_min_duration_statement = 500
```

## Monitor SQL queries

```
pip install pg_activity
su - postgres -c "pg_activity"
```

## Vacuum databases

```
# vacuum all databases every night (full vacuum on Sunday night, lazy vacuum every other night)
45 3    * * 0       nice -n 19 su - postgres -c "vacuumdb --all --full --analyze"
45 3    * * 1-6     nice -n 19 su - postgres -c "vacuumdb --all --analyze --quiet"
```
