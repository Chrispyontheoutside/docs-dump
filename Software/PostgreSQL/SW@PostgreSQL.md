# PostgreSQL

## Description

PostgreSQL is a powerful, open source object-relational database system.

  - Homepage: <https://www.postgresql.org//>

## Access

PostgreSQL is open to all HPRC users.

### PostgreSQL Module

TAMU HPRC currently supports the user of PostgreSQL though the
PostgreSQL modules. There are several PostgreSQL modules available on
Ada and Terra.

You can learn more about the module system on our
[SW:Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.

### PostgreSQL on Ada

`(1) module load PostgreSQL/11.3-GCCcore-8.2.0-Python-2.7.15`  
`(2) initdb -D $SCRATCH/postgresql/my_psql_db`  
`(3) pg_ctl -o "-p 9999" -D $SCRATCH/postgresql/my_psql_db -l $SCRATCH/postgresql/my_psql_db.log start`  
`       # comment: the -o provides extra options. In this example, the extra option is the port by -p`  
`       # The -D option specifies the postgresql database directory.`  
`       # The -l option specify the log file for the database instance.`  
`(4) createdb employee -p 9999         # create a database named employee`  
`(5) psql -d employee -p 9999          # connect to employee database on port 9999`  
`(6) execute your sql statements in psql; type exit to exit psql prompt`  
`(7) pg_ctl -D $SCRATCH/postgresql/my_psql_db stop  # stop the database`

You may set password for your database if it is needed. These are the
commands for the first time set up of PostgresSQL. After this, you only
need to start the server, connect to it, and stop it, i.e., step (3),
(5), (6) and (7). You only need to initdb (step 1), createdb (step 4)
for one time.

Note: the database directory and name, database username, and port
should be changed by users.

If you see a message like the following, check the logfile
(my\_psql\_db.log in this example) you may have forgotten to stop your
postgresql server on the specified port (9999 in this example) or
another user is using the specified port. If someone else is using port
9999, you can try port 9998.

    waiting for server to start.... stopped waiting
    pg_ctl: could not start server
