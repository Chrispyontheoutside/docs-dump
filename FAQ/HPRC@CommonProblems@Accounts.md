# Accounts

### Q: When do accounts expire?

**A:** Accounts expire at the start of the new fiscal year (September
1st). You can see when your account expires by going to our [Account
Management System (AMS)](https://hprc.tamu.edu/ams/) and checking under
the Accounts tab.

### Q: How do I get more SUs?

**A:** Students will need to have their PI transfer SUs to them. PIs can
apply for up to two Startup accounts, each for up to 200,000 SUs and for
not more than 400,000 collective SUs. After this Startup allocation has
run out, PIs will need to apply for a Research allocation. More
information on the allocation policies can be found on our [Account
Allocations](https://hprc.tamu.edu/policies/allocations.html) page.

### Q: I just received my SUs, how can I use them?

**A:** When you have received your SUs, you will need to either
change/set your default account or request in your job file that a
certain account will be used.

  - To change your defualt account, use the myproject utility on our
    systems. More information on the myproject utility can be found on
    our [ AMS User Interface](/kb3/User-Guides/AMS-Documentation/HPRC@AMS@UI/ "wikilink") page. Also see on
    [ my project page](/kb3/Helpful-Pages/myproject/HPRC@myproject/ "wikilink").

`[NetID@cluster ~]$  myproject -d XXXXXXXXXX`  
`Your default project account now is XXXXXXXXXX.`

  - To request a certain account in your job file, add the following
    line to the directives section of your job file:

**On Terra:**

`#SBATCH -account=XXXXXXXXXX`

### Q: How do I set my default account?

**A:** When you have received your SUs, you will need to either
change/set your default account or request in your job file that a
certain account will be used.

  - To change your defualt account, use the myproject utility on our
    systems. More information on the myproject utility can be found on
    our [ AMS User Interface](/kb3/User-Guides/AMS-Documentation/HPRC@AMS@UI/ "wikilink") page. Also see on
    [ my project page](/kb3/Helpful-Pages/myproject/HPRC@myproject/ "wikilink").

`[NetID@cluster ~]$  myproject -d XXXXXXXXXX`  
`Your default project account now is XXXXXXXXXX.`

  - To request a certain account in your job file, add the following
    line to the directives section of your job file:

**On Terra:**

`#SBATCH -account=XXXXXXXXXX`

### Q: How do I transfer SUs?

**A:** To transfer SUs, PIs will need a Startup or Research allocation
(see our [Account
Allocations](https://hprc.tamu.edu/policies/allocations.html) page for
more information). Once an account has been granted to the PI, they can
transfer SUs to any of their researchers on our [Account Management
System (AMS)](https://hprc.tamu.edu/ams/). If a PI needs to add a new
researcher, the PI must [contact the Help
Desk](https://hprc.tamu.edu/about/contact.html).

### Q: How long will I be able to access HPRC after losing status as a TAMU student/employee?

**A:** All critical data should be backed up prior to your TAMU status
transitioning in any way. As soon as a system member's status switches
to inactive, their NetID is locked. Former employees may be extended the
professional courtesy of extended NetID use for up to one year for valid
purposes. In the case where extended use of a NetID account is
warranted, a sponsor (such as the former employee's department, or
former student's professor) must submit a NetID request form. This
process is detailed below.

### Q: How do I get a Guest NetID account for myself or my researchers?

**A:** Guest NetID accounts are handled by the Identity Management
Office. The [Guest NetID Account Request
Form](http://infrastructure.tamu.edu/identity/forms/NetIDAccountRequestForm.pdf)
should be submitted to the Identity Management Office. There are
different ways you can submit the form described in the second paragraph
of the form.

You will need to specify start and stop affiliation dates on the Guest
NetID Request Form. These dates may or may not coincide with HPRC
account renewal dates depending on what you list and what gets approved.
This Guest NetId Account Request Form is handled by a different
department on campus and is separate from the HPRC application. The HPRC
application is the one you need to renew with us each year (September 1
- August 31). You must fill out the Guest NetID Account Request Form
prior to applying for an HPRC account.

If the person using the Guest NetID intends to user TAMU Wi-Fi or the
[TAMU VPN](https://u.tamu.edu/KB0010938) (off campus access), those
resources must be requested on the Guest NetID Account Request Form.

### More information regarding Extended Account Access

For more information regarding extension of netID, please refer to this
[document](http://u.tamu.edu/lifecycle). Information regarding Extended
Account Access can be found on page 13.