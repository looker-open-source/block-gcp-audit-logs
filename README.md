### What can I do with this Looker Block?
**(1) Use pre-built dashboards to quickly analyze and alert on GCP Audit log data** - Dashboards include an Admin Activity overview, an account investigation dashboard, and a dashboard that uses the MITRE ATT&CK framework to view activities that map to attack tactics.

**(2) Easily explore and query GCP Audit Log data** - This block contains Explores for the Admin Activity and Data Access tables. These Explores allow you to build custom queries, build additional reports and dashboards, and set up threshold alerts on any of these fields or associated metrics.

**(3) Extend the model for further analysis** - This project is likely a starting point for your own SOC. The model can be extended with metrics specific to your organization on the audit log data. It can also be extended to include analysis of any other log type. Looker can effectively be used as a SIEM tool for historical (vs real-time) analysis. Threshold alerts can be run at 5-minute increments and data can be queried as fast as it is landed in BigQuery.

**(4) Use as part of an Enterprise Data Platform** - Take advantage of Looker's data platform functionality, including [data actions](https://looker.com/platform/actions), scheduling, permissions, alerting, parameterization (each user can only see their own data), and more.


### GCP Security Data Structure

* GCP Audit Logs consist of Admin Activity, Data Access, System Events, and Policy Denied logs. This block is built on the mostlogs commonly used for analytics, Admin Activity and Data Access. Docs on these logs are [found here](https://cloud.google.com/logging/docs/audit).

* GCP logs can be exported to BigQuery using [Aggregated Sinks](https://cloud.google.com/logging/docs/export/aggregated_sinks) in [Cloud Logging](https://cloud.google.com/logging), This will allow you to create export log entries from all the projects, folders, and billing accounts of a Google Cloud organization.

* Exporting involves writing a filter that selects the log entries you want to export and choosing a destination.  To use this block, you will send the logs to tables created in [BigQuery](https://cloud.google.com/bigquery) datasets. For instructions on how to do this please follow this [link](https://cloud.google.com/logging/docs/export)

* Recommended Filter:
`protoPayload.@type=type.googleapis.com/google.cloud.audit.AuditLog`



### Block Structure

* The ``access`` and ``activity`` views are the foundation of this block and the other views are used for supplemental analysis: a derived table for IAM analysis, an IP geo lookup view, and derived tables used to identify failed access attempts followed by a grant. The model file defines some simple explores. This block uses some SQL specific to BQ to unnest and handle structs, arrays, and JSON data.

* This block utilizes Refinement files for customization. For more information on using refinements to customize marketplace blocks, please see [this documentation](https://docs.looker.com/data-modeling/marketplace/customize-blocks).


### Further analysis in consideration for a future version of this block

* VPC Flow log model and content

* Data Access content

* Other high-value and broadly-applicable analytics use cases we identify in the field

# IMPORTANT NOTE: NEWER AUDIT LOG BLOCK NOW AVAILABLE
#### Apr 2023 - This block leverages the older "log sink" to BigQuery methodology. There is a new and improved "Log Analytics" method that would be recommended for any new projects going forward. [Compare the 2 methods here](https://cloud.google.com/blog/products/data-analytics/moving-to-log-analytics-for-bigquery-export-users).
#### Please refer to the new [Cloud Logging - Log Analytics](https://marketplace.looker.com/marketplace/detail/cloud-logging) block for the updated lookml and dashboards.
