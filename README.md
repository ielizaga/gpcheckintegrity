# gpcheckintegrity
Utility for Greenplum Database that performs a table integrity exam to verify that all the tables in a specific database can be queried. 

## Purpose
The purpose of this tool is to be able to detect when any of the segments in Greenplum have a bad copy of a table file(s). This is an issue that can happen when there is disk corruption in any of the nodes of the cluster and a disk repair utility is ran (i.e. xfs_repair, fsck)

## How does it work
This tool will go through each and every table of a specific database and perform a PostgreSQL [COPY](http://www.postgresql.org/docs/9.1/static/sql-copy.html) command to in all segments to verify the table can be queried in the whole cluster. 

```
COPY example_table TO '/dev/null'
```

## Ongoing work
- [x] Check table integrity in one database secuentially
- [ ] Check table integrity in multiple databases
- [x] Check table integrity in one database in parallel
- [x] Check table integrity in just one schema
- [ ] Check integrity in just one table
- [ ] Detailed report of the exam
- [ ] Specify number of threads spawned in the cluster in parallel
- [ ] Help -? functionality
- [ ] User prompts
- [ ] Exam progress information




