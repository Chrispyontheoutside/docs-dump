# RCS

RCS (Revision Control System) is very useful for small groups wanting to
operate on and update common files. It provides a way to "lock" files
while changes are made and provides a method to document why changes
were made.

For the best explanation see the **man** page:

`man rcsintro`

That is the best place to get an overview.

Typical use will be something like:

` co -l filename  # check out file from RCS with a lock`  
` # vi/edit filename (make changes)`  
` ci -m"I made this change" filename  # check file back in to RCS to remove lock... provide a message to explain changes`  
` co filename # after you do "ci" it won't be in present directory anymore, check it out without a lock`

Failure to remove the lock will result in other members in your group
not being able to make changes to it.

For groups wanting to share files, we recommend the directory with the
files and RCS directory within have 2770 permissions for the group

Useful tools include **rcsdiff** (show differences between different
versions) and **rcslog** (describes changes made)

For more information see more of the **man** pages (listed at the bottom
of the above **man** page under the SEE ALSO section) or many of the
hundreds of pages available via Google.
