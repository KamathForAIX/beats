::::{warning}
This functionality is in beta and is subject to change. The design and code is less mature than official GA features and is being provided as-is with no warranties. Beta features are not subject to the support SLA of official GA features.
::::


`sysmetric` Metricset includes the system metric values captured for the most current time interval from Oracle System View.

This metricset dynamically filters metrics based on given input `patterns`. These patterns can be keywords or regular expressions. The `sysmetric` metricset uses the `OR` operator when forming the SQL query internally. Refer [here](https://docs.oracle.com/cd/B12037_01/server.101/b10759/conditions016.htm) for more details. `V$SYSMETRIC` table provides different metrics for a short duration (15 seconds, `GROUP_ID` 3) and a long duration (60 seconds, `GROUP_ID` 2). This metricset collects metrics which have `GROUP_ID` 2 i.e. the metrics that are queried for long-duration for DBAs to use the data for historical analysis.

**Note**: As the value of the metrics queried for long-duration in the `V$SYSMETRIC` table is updated every 60 seconds, it is recommended for the users to set the collection period in the configuration for sysmetric metricset as greater than or equal to 60 seconds so as to avoid duplication of the metrics in the ingested events.


## Required database access [_required_database_access_2]

To ensure that the module has access to the appropriate metrics, the module requires that you configure a user with access to the following tables:

* V$SYSMETRIC


## Example event [_example_event]

```
{
  "@timestamp": "2022-05-27T02:18:55.112Z",
  "event": {
    "dataset": "oracle.sysmetric",
    "module": "oracle",
    "duration": 408974115
  },
  "metricset": {
    "name": "sysmetric",
    "period": 60000
  },
  "oracle": {
    "sysmetric": {
      "metrics": {
        "physical_write_total_bytes_per_sec": 15323.3127812031,
        "total_table_scans_per_txn": 40,
        "physical_read_total_bytes_per_sec": 40680.153307782,
        "total_pga_allocated": 2.364416e+08
      }
    }
  },
  "service": {
    "address": "oracle://localhost:1521/ORCLCDB.localdomain",
    "type": "oracle"
  }
}
```
