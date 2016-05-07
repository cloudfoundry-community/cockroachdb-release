# CockroachDB BOSH Release

BOSH release of CockroachDB, a distributed SQL database built on a transactional and strongly-consistent key-value store

## Quick Start for [BOSH Lite](https://github.com/cloudfoundry/bosh-lite)

1. Target your BOSH Lite director with your BOSH CLI.
2. Upload a *cloud-config* to your director, e.g.
```bash
bosh update cloud-config examples/cloud-config-bosh-lite.yml
```
3. Create your release and upload it, e.g.
```bash
bosh create release --force
bosh upload release
```
4. Modify your deployment manifest to include your BOSH's UUID:
```bash
bosh status --uuid
vim examples/cockroachdb-bosh-lite.yml # update UUID
```
5. Deploy
```
bosh deployment examples/cockroachdb-bosh-lite.yml
bosh deployment
```
6. Check the web interface, e.g. [http://10.244.0.2:8080/#/cluster](http://10.244.0.2:8080/#/cluster)
7. Run SQL commands against the CockroachDB cluster:
```bash
cockroach sql --host 10.244.0.2
```
```sql
root@10.244.0.6:26257> show tables;
root@10.244.0.6:26257> create table example_table (id int, name text);
root@10.244.0.6:26257> insert into example_table values (1,'hi');
root@10.244.0.6:26257> select * from example_table;
+----+------+
| id | name |
+----+------+
|  1 | hi   |
+----+------+
```
