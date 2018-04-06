# High availability database in the cloud

## Option 1 : 2 instances with semisynchronous replication


Database 1 in region A
Database 2 in region B

Initiate a fail over when it is detected that a database is not responding.

Example 30 seconds timeout during 5 minutes.

The way this kind of high availability is set up depends on the Database vendor.

For MySQL there is a Master High Availability manager (MHA).

