# Functionality

## Manage your accounts

Manage your granted computing time and report your usage with AMS. AMS
allows you to flexibly manage the computing time you have been granted
for each the different machines of our Supercomputing Facility upon
approval of your application.

Computing time is granted and measured in **service units (SUs)**. Each
SU corresponds to 1 hour of wall clock time elapsed on 1 cpu-core by
your application. The amount of resources used by your jobs is deducted
from a **project account**.

A personal **project account** is created for each machine requested in
your application when you apply for the first time. A project account
allows you to keep track of all the SUs granted to you and used by you
on a given machine. It is usually assigned to you for the duration of
your project, but it expires at the end of each **accounting period**.
Currently, an **accounting period** spans an entire school year, running
from September 1<sup>st</sup> to August 31<sup>st</sup> of the next
year. For such reason, we will refer to it as **fiscal year (FY)**.

For your convenience, project accounts are tied to the reason of your
request of computing time. Therefore, you may assign to your project
account a description related to your intended usage of the machine. For
instance, you may use the title of a personal research project, or
mention a class you are attending, etc.

If you reapply in the near future for the same research project, you may
be allowed to continue to use the same project account number assigned
to you for that project during the previous accounting period.

If you are a **Principal Investigator (PI)**, and you manage a group of
users working on a single research project, you may transfer SUs to your
researchers' project accounts using your AMS personal web interface. You
may also reclaim your transferred SUs and redistribute them later on
according to your needs.

You should always select which one of your project accounts you wish to
use.

For your convenience, however, you may designate a **primary** project
account, which will be used as your default account when you don't
specify any account number. Currently, you may only set your primary
account using the command line interface (**myproject -d
accountnumber**).

If you have only one project account, then this account is automatically
set as primary and your usage is deducted from it by default.

Once you submit a job to our batch system, AMS computes an amount in SUs
based on the amount of resources (wall clock time and number of cpu
cores) requested by your batch job file. The balance of your selected
project account is then checked to determine if you have enough SUs left
to accommodate this amount (This check is done for each job step
included in your job command file on eos). If your available balance is
large enough, the amount is posted to the project account as
**pending**. Once your job has exited the batch system, this pending
amount is dismissed and a new amount reflecting the actual usage is
deducted as **final**.

If your project account does not contain enough SUs to satisfy what
requested in your job command file, your job submission will be rejected
by the batch system until your account will be replenished.

For such reason, we strongly encourage you to request an amount of
resources very close to what you estimate your job will actually need.

Also, you will not be allowed to use the batch system after your project
account has expired. However, you may continue to login on the system
and work on your files until your login id expires.

Currently, the expiration date of your login id is set by default to
October 1<sup>st</sup>.
