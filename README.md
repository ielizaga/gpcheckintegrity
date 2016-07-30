# gpcheckintegrity
Utility for Greenplum Database that performs a table integrity exam to verify that all
the tables in a specific database can be queried.

## Purpose
The purpose of this tool is to detect when any of the segments in Greenplum
have a bad copy of a table file(s). This is an issue that can happen when there is disk
corruption in any of the nodes of the cluster and a disk repair utility is ran
(i.e. xfs_repair, fsck)

## How does it work
This tool will go through each and every table of a specific database and perform a
PostgreSQL [COPY](http://www.postgresql.org/docs/9.1/static/sql-copy.html) command to
/dev/null in all segments to verify the table can be queried in the whole cluster.

```
COPY example_table TO '/dev/null'
```

## Installation
Simply download the python file `gpcheckintegrity` into your system and run it!

Try the latest dev version in the repo:

```
$> curl -L -o gpcheckintegrity https://raw.githubusercontent.com/ielizaga/gpcheckintegrity/master/gpcheckintegrity
$> ./gpcheckintegrity --help
```

## Usage

Check integrity of database `<database>`. Options to filter by schema and to control parallelism available. 

```
gpcheckintegrity [-v | --verbose] [-s | --schema <schema_name> ] [-B | --parallel <threads>] {-d | --database} <database>
```


Check integrity in all the databases

```
gpcheckintegrity -A
```


Print help message

```
gpcheckintegrity -h | -? | --help
```

## Examples

Check all the tables in all databases:

`gpcheckintegrity -A`

Check the integrity of all the tables in the database 'sales':

`gpcheckintegrity -d sales`

Check the integrity of all the tables in 'division_1' from DB 'sales':

`gpcheckintegrity -s division_1 -d sales`

Display help message:

`gpcheckintegrity -h`
