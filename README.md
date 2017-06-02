# pgimport

Import data from file to PostgreSQL database.


## Installation

```sh
$ npm install pgimport -g
```

## Usage

```sh
$ pgimport

  Usage: pgimport [options]

  Options:

    -h, --help                     output usage information
    -v, --version                  output the version number
    --connect <connect>            Db connection string
    --from <from>                  Source folder or file
    --to <to>                      Destination table
    --local-dir <local_dir>        Local directory where remote files are synced, default=/tmp/pgimport
    --access-key <access_key>      AWS access key
    --secret-key <secret_key>      AWS secret key
    --ignore-attrs <attrs_list>    Ignore attributes
    --map <map_file>               File path containing the attribute/field mapping
    -p, --processors <processors>  Number of processors, default=1
    -r, --recursive [true|false]   Recursive copy, default=false
    -f, --force [true|false]       Non-interactive, default=false
    -d, --debug [true|false]       Show debug messages, default=false


$ pgimport --connect='user@localhost' --to='public.logs' --from='/path/to/file.log'
$ pgimport --connect='user@localhost' --to='public.logs' --from='/path/to/file.log.gz'
$ pgimport --connect='user@localhost' --to='public.logs' --from='s3://bucket/folder' -r -f
```

## File Format

Data records should be in a valid JSON format. Each line represents a row in the database table with JSON attribute names as column names.

```sh
$ cat sample.log
{ "ts":"2017-06-01T01:14:09Z", "event":"pageview", "url":"http://www.abc.com" }
{ "ts":"2017-06-01T01:39:51Z", "event":"pageview", "url":"http://www.def.com" }
{ "ts":"2017-06-01T02:11:47Z", "event":"pageview", "url":"http://www.ghi.com" }
```

## Database Connection String

The general form for a connection string:

```sh
[user[:password]@][netloc][:port][/dbname][?param1=value1&...]
```
Examples:

```sh
localhost
localhost:5433
localhost/mydb
user@localhost
user:secret@localhost
other@localhost/otherdb?connect_timeout=10
```
