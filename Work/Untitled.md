```promql
(
  sum by (jobName, env) (
    delta(
    # rate/delta were removing __name__ label, this is a workaround for this
      label_replace(
      # query for all IB data platform ingestion job successful executions
        {tenant="shield-ib", __name__=~".*information_barrier.*_executions_successful_count", metric_type="counter"}
        , "jobName", "${1}", "__name__", "data_platform_jobs_(information_barrier.*)_executions_.*_count"
      )[1h:] # label_replace
    ) # delta
  ) # sum
    <bool 1 # sum of successful jobs < 1
) + on(jobName, env) 
(
  sum by (jobName, env) (
    delta(
    # rate/delta were removing __name__ label, this is a workaround for this
      label_replace(
      # query for all IB data platform ingestion job successful executions
        {tenant="shield-ib", __name__=~".*information_barrier.*_executions_failed_count", metric_type="counter"}
        , "jobName", "${1}", "__name__", "data_platform_jobs_(information_barrier.*)_executions_.*_count"
      )[1h:] # label_replace
    ) # delta
  ) # sum
    >bool 0 # sum of failed job > 0
) >=bool 2 # if (sum of failed jobs > 0 && sum of successful jobs < 1) then true (so fire alert)
```
