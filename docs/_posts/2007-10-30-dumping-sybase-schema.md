---
permalink: /2007/10/30/dumping-sybase-schema
date: '2007-10-30 12:19:00'
title: >-
    dumping sybase schema
---

currently i have a privilege to work with sybase 12.5. perhaps i am
spoiled with the ease of `mysqldump db_name [tables]` or
`echo .dump [tables] | sqlite3`, but i expect any modern database to
have a scriptable way to dump schema for selected tables in `create`
statements, as well as data in `insert` statements that simply could be
piped back when needed.

while dumping data is easy enough using `bcp`, scriptable schema
extracts are a bit trickier (especially if you want it to be
cross-platform).

but we are lucky – it took sybase only 20+ years to introduce a
command-line utility written in java called `ddlgen` in version 15 of
its flagship enterprise product (in my case it worked against 12.5 as
well).

# ddlgen

-   rip it out from freely downloadable [developers’ distro of
    sybase](http://www.sybase.com/products/databasemanagement/adaptiveserverenterprise)

<!-- -->

    $ ls -lR c:/programs/sybase/ddlgen/
    c:/programs/sybase/ddlgen/:
        ddlgen.sh
        lib/

    c:/programs/sybase/ddlgen/lib:
        DDLGen.jar
        dsparser.jar
        jconn3.jar

-   rig up the wrapper script:

```sh
    $ cat c:/programs/sybase/ddlgen/ddlgen.sh 
    JAVA_HOME=c:/programs/java/jdk/jdk1.6.0_03
    LIB_DIR=`dirname $0`/lib
    CLASSPATH=$LIB_DIR/jconn3.jar:$LIB_DIR/dsparser.jar:$LIB_DIR/DDLGen.jar

    $JAVA_HOME/bin/java \
    -mx500m \
    -classpath `cygpath --mixed --path $CLASSPATH` \
    com.sybase.ddlgen.DDLGenerator $*
```

# backup scripts

-   `schema-out.sh`

```sh
    source env.sh

    [ ! -d $OUT_DIR ] && mkdir -p $OUT_DIR

    for table in $TABLES; do
        out_file=`cygpath --mixed --absolute $OUT_DIR/${table}-schema.txt`
        printf "dumping $table schema to $out_file... " 
        $DDLGEN -U $USERNAME -P $PASSWORD -S $SERVER:$PORT -D $DATABASE -TU -N$table -O $out_file
        printf "done\n" 
    done
```

-   `bcp-out.sh`

```sh
    source env.sh

    [ ! -d $OUT_DIR ] && mkdir -p $OUT_DIR

    LOG=`dirname $0`/bcp-out.log
    cat /dev/null > $LOG

    for table in $TABLES; do
        out_file=`cygpath --mixed --absolute $OUT_DIR/${table}-bcp.txt`
        printf "dumping $table to $out_file... " 
        bcp $DATABASE.dbo.$table out $out_file -c -t, -S $SERVER -U $USERNAME -P $PASSWORD >> $LOG
        printf "done\n"
    done
```

-   `schema-in.sh`

```sh
    source env.sh

    LOG=`dirname $0`/schema-in.log
    cat /dev/null > $LOG

    for table in $TABLES; do
        in_file=`cygpath --mixed --absolute $OUT_DIR/${table}-schema.txt`
        [ ! -f $in_file ] && echo "$in_file does not exist for $table, skipping" && continue
        printf "loading $table schema from $in_file... " 
        isql -S$SERVER -U$USERNAME -P$PASSWORD < $in_file >> $LOG
        printf "done\n" 
    done
```

-   `bcp-in.sh`

```sh
    source env.sh

    [ ! -d $OUT_DIR ] && mkdir -p $OUT_DIR

    LOG=`dirname $0`/bcp-in.log
    cat /dev/null > $LOG

    for table in $TABLES; do
        in_file=`cygpath --mixed --absolute $OUT_DIR/${table}-bcp.txt`
        [ ! -f $in_file ] && echo "$in_file does not exist for $table, skipping" && continue
        printf "loading $table from $in_file... " 
        bcp $DATABASE.dbo.$table in $in_file -c -t, -S $SERVER -U $USERNAME -P $PASSWORD >> $LOG
        printf "done\n" 
    done
```

do i feel silly? yes. do i feel petty? yes. does it make me feel better
about myself, given that the sybase DBA told
me to contact dbartisan support to see if i could script their tool to
do this? oh yes.
