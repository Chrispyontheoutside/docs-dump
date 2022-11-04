# AMS User Interfaces

AMS provides two different interfaces to users: web interface and
command line.

### Web Interface

The [web interface](https://hprc.tamu.edu/ams/) provides a complete and
historical view of your HPRC resources.

### Command Line

The command-line interface may be accessed by a command on the login
nodes of a cluster. Also see on [ **myproject**
page](/kb3/Helpful-Pages/myproject/HPRC@myproject/ "wikilink").

## Grace and Terra

On Grace and Terra, the command is "myproject -h" which provides the
help information listed below:

    myproject -h
         -d accountNo: Set accountNo as the default project account
             -e YYYY-MM-DD: Specify end date (00:00 AM) for job records
                        (-j option must be specified.)
             -h: Display this help and exit.
         -j accountNo (or 'all'): Produce the job records in current fiscal year for 
             the selected project account or all project accounts when 'all' is given.
         -l: List all the active local project accounts.
         -p accountNo: List uncomplted jobs for accountNo.
             -s YYYY-MM-DD: Specify start date (00:00 AM) for job recrods.
                        (-j option must be specified.)
             -c: Display job records with line length <= 80 chars.
                        (-j option must be specified.)

Examples below show the most common usage of "myproject" command:

### Example 1: List all accounts

The "-l" option list all projects for the user on Grace.

`   [user@grace ~]$ `**`myproject   -l`**  
`  ==========================================================================================`  
`               List of user's Project Accounts`  
`------------------------------------------------------------------------------------------`  
`|  Account   | Default | Allocation |Used & Pending SUs|   Balance  |          PI         |`  
`------------------------------------------------------------------------------------------`  
`|1328000223136|        N|    10000.00|              0.00|    10000.00|Doe, John           |`  
`------------------------------------------------------------------------------------------`  
`|1328000243716|        Y|     5000.00|            -71.06|     4928.94|Doe, Jane           |`  
`------------------------------------------------------------------------------------------`  
`|1358000247058|        N|     5000.00|             -0.91|     4999.09|Doe, Jane           |`  
`------------------------------------------------------------------------------------------`

### Example 2: Set Default Account

The "-d xxxxxxx" sets the project account xxxxxxx to be the default
account to be charged when jobs are submitted by the user. The default
project account can be overridden by "\#SBATCH -A yyyyyy" in a job
script for a particular job.

`   [user@terra ~]$ `**`myproject   -d   122858321140`**  
`   Your default project account now is 122858321140.`

### Example 3: List Completed Jobs

The "-j" option list jobs completed on Grace or Terra. If the extra "-s"
and "-e" option are not specified, all jobs in current fiscal year
(starting from 9/1 to 8/31 next year) are listed.

`   [user@grace ~]$ `**`myproject   -j   132858329759`**  
`   ------------------------------------------------------------ List of Jobs --------------------------------------------------------------------- `  
`   |ProjectAccount|    JobID    |JobArrayIndex|     SubmitTime     |      StartTime     |      EndTime       | Walltime | TotalSlots |  UsedSUs   |`  
`   ----------------------------------------------------------------------------------------------------------------------------------------------- `  
`   |132858329759  |1739566      |0            |2015-09-14 15:18:16 |2015-09-14 15:18:16 |2015-09-14 15:18:27 |        11|           1|        0.00|`  
`   |132858329759  |1739567      |0            |2015-09-14 15:18:32 |2015-09-14 15:18:33 |2015-09-14 15:28:41 |       608|           1|        0.17|`  
`   |132858329759  |1739568      |0            |2015-09-14 15:18:42 |2015-09-14 15:18:42 |2015-09-14 15:19:09 |        27|           1|        0.01|`  
`   |132858329759  |1739569      |0            |2015-09-14 15:18:43 |2015-09-14 15:18:44 |2015-09-14 15:19:15 |        31|           1|        0.01|`  
`   |132858329759  |1739570      |0            |2015-09-14 15:18:44 |2015-09-14 15:18:45 |2015-09-14 15:18:55 |        10|           1|        0.00|`  
`   |132858329759  |1739578      |0            |2015-09-14 15:20:31 |2015-09-14 15:20:33 |2015-09-14 15:20:40 |         7|           1|        0.00|`  
`   |132858329759  |1739579      |0            |2015-09-14 15:20:42 |2015-09-14 15:20:43 |2015-09-14 15:22:01 |        78|           1|        0.02|`  
`   |132858329759  |1739580      |0            |2015-09-14 15:20:46 |2015-09-14 15:20:47 |2015-09-14 15:20:54 |         7|           1|        0.00|`  
`   |132858329759  |1739581      |0            |2015-09-14 15:20:47 |2015-09-14 15:20:48 |2015-09-14 15:20:55 |         7|           1|        0.00|`  
`   |132858329759  |1739582      |0            |2015-09-14 15:20:48 |2015-09-14 15:20:49 |2015-09-14 15:20:57 |         8|           1|        0.00|`  
`   |132858329759  |2259750      |0            |2016-03-07 12:46:13 |2016-03-07 12:46:15 |2016-03-07 13:28:55 |      2560|           1|        0.71|`  
`   |132858329759  |2259751      |0            |2016-03-07 12:46:15 |2016-03-07 12:46:16 |2016-03-07 13:28:54 |      2558|           1|        0.71|`  
`   |132858329759  |2259752      |0            |2016-03-07 12:46:17 |2016-03-07 12:46:18 |2016-03-07 12:56:01 |       583|           1|        0.16|`  
`   |132858329759  |2259753      |0            |2016-03-07 12:46:19 |2016-03-07 12:46:20 |2016-03-07 12:55:59 |       579|           1|        0.16|`  
`   |132858329759  |2259754      |0            |2016-03-07 12:46:21 |2016-03-07 12:46:22 |2016-03-07 12:49:27 |       185|           1|        0.05|`  
`   |132858329759  |2259755      |0            |2016-03-07 12:46:24 |2016-03-07 12:46:25 |2016-03-07 12:49:27 |       182|           1|        0.05|`  
`   |132858329759  |2259756      |0            |2016-03-07 12:46:26 |2016-03-07 12:46:26 |2016-03-07 12:47:38 |        72|           1|        0.02|`  
`   |132858329759  |2259757      |0            |2016-03-07 12:46:28 |2016-03-07 12:46:28 |2016-03-07 12:47:38 |        70|           1|        0.02|`  
`   |132858329759  |2261528      |0            |2016-03-08 11:05:32 |2016-03-08 11:05:33 |2016-03-08 11:05:36 |         3|           1|        0.00|`  
`   |132858329759  |2261530      |0            |2016-03-08 11:06:08 |2016-03-08 11:06:09 |2016-03-08 11:06:14 |         5|           1|        0.00|`  
`   |132858329759  |2261547      |0            |2016-03-08 11:07:34 |2016-03-08 11:07:35 |2016-03-08 11:08:15 |        40|           1|        0.01|`  
`   |132858329759  |2261550      |0            |2016-03-08 11:07:55 |2016-03-08 11:07:56 |2016-03-08 20:08:03 |     32407|           1|        9.00|`  
`   |132858329759  |2261694      |0            |2016-03-08 11:59:49 |2016-03-08 11:59:50 |2016-03-08 12:00:17 |        27|           1|        0.01|`  
`   ------------------------------------------------------------------------------------------------------------------------------------------------ `  
`                                                                                                   |Total Jobs: 1021      |Total Usage: 1220.41   |`  
`   ------------------------------------------------------------------------------------------------------------------------------------------------`

### Example 4: List Incomplete Jobs

The "-p" option lists the pending (incomplete jobs) pre-charged to the
project specified for this option. The pre-charged SUs listed in the
output will be removed after the jobs are completed, and those completed
jobs will be charged by their actual used SUs.

`   [user@terra ~]$ `**`myproject   -p   122858329759`**  
`   --------------------------------------------------------------------`  
`   |   Job Id   |State|#Cores|#EffectiveCores|Walltime(H)|Pending SUs|`  
`   --------------------------------------------------------------------`  
`                  |Total Jobs: 0      |Total Pending SUs: 0.00        |`  
`   --------------------------------------------------------------------`
