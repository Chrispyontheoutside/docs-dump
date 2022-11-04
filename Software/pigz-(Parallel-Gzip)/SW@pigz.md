# pigz

[pigz](https://zlib.net/pigz/) (**p**arallel **i**mplementation of
**gz**ip) is a fully functional replacement for gzip that exploits
multiple processors and multiple cores when compressing data. pigz is
extremely helpful when compacting a large directory. unpigz (equivalent
to 'gunzip') is used to uncompress gzip'ed file and unpigz utilizes only
one thread.

pigz can be accessed by loading a pigz module (run "module spider pigz"
to find the module name). On FTN nodes, pigz is available without
loading the module.

### Simple examples

  - Compress a file

<!-- end list -->

    pigz my_file

  - Compress a file with best compression rate

<!-- end list -->

    pigz -9 my_file
    pigz --best my_file

  - Uncompress

<!-- end list -->

    unpigz my_file.gz

  - Specify number of threads ('-p no\_thread'). The number of compress
    threads is set by default to the number of online processors.

<!-- end list -->

    pigz -9 -p 10 my_big_file

### Using tar with pigz

  - specify compress program for tar

<!-- end list -->

    tar -I pgz cf my_dir.tar.gz my_dir/
    tar --use=compress-program pigz my_dir.tar.gz my_dir/

  - specify more options with pigz

<!-- end list -->

    tar cf - my_dir/ | pigz -9 > my_dir.tgz
    tar cf - my_dir1 my_dir2 | pigz -9 -p 15 > my_backup.tgz

### Speed comparison

The following example shows speed difference between gzip and pigz on
CentOS 7 ISO file (~ 11GB) on Terra server (28 cores, 2.4 GHz, with
hyper-thread enabled). The time for best compression (-9) was about 27
sec (pigz) vs 6 min 6 sec (gzip), where pigz was about 13 times faster
than gzip. pigz used 58 threads with 2361% CPU, which was equivalent to
2.361 cores (out of 28 cores).

    $ ls -l *.iso
    -rw-rw-r--  1 user1 user1 11026825216 Dec 16 12:26 CentOS-7-x86_64-Everything-1908.iso
    
    $ time gzip -9 CentOS-7-x86_64-Everything-1908.iso
    real    6m6.302s
    user    5m51.763s
    sys     0m27.914s
    
    $ time pigz -9 CentOS-7-x86_64-Everything-1908.iso
    real    0m26.987s
    user    9m9.098s
    sys     0m19.994s
    
    $ ls -l *.iso.gz
    -rw-rw-r--  1 user1 user1 10653982882 Dec 16 12:26 CentOS-7-x86_64-Everything-1908.iso.gz

### References

  - pigz home page: <https://zlib.net/pigz/>
  - pigz manual page: <https://zlib.net/pigz/pigz.pdf>
  - some speed test results: <https://rachaellappan.github.io/pigz/>
