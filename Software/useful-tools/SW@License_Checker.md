# License Status Check
A license status check tool, **license_status**, has been added to Ada in order to allow users to check if there are licenses available for any particular licensed software on our clusters.

To see the various options available, use the -h option:

```php
[user@terra ~]$ license_status -h
   Usage: ./license_status [option list...]
   
   Options:
       -l: List all names that can be used with the -s option.
       -a: List the license status for all software supported by this script.
       -s NAME: List the license status for software NAME.
       -h: Display this help.
```

To check on the license status of a particular software, use the -s option:

```php
   [user@terra ~]$ license_status -s ansys
   License status for ANSYS:
   ---------------------------------------------------------------
   |License Name               |  # Issued|  # In Use|# Available|
   ---------------------------------------------------------------
   |aa_mcad                    |        50|         0|         50|
   |aa_r                       |        50|        32|         18|
   |aim_mp1                    |        50|         0|         50|
   |aa_r_hpc                   |       128|       100|         28|
   ---------------------------------------------------------------
```

To see the license status for all available software, use the -a option:

```php
[user@terra ~]$ license_status -a
```

To see the software supported by this tool, use the -l option:

```php
[user@terra ~]$ license_status -l
```
