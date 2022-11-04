# Terra Debugging 


## A Note on Terra Usage

<font color=teal> This page was originally written for usage on Ada.

Most of the content on this page is applicable to Terra. Some
modifications to modules, directories, or other non-major concepts may
be needed. </font>

## Debugging Programs with "idb"

"idb" is Intel's integrated debugging environment which can be used with
either its GUI or its command line front end. We assume that the
compiler environment has been prepared.

To be able to debug code developed with the Intel compilers, you should
use the "-debug" flag in the compilation command line. It is best to
avoid any optimization and thus you need to specify the "-O0" as well.

## Simple "helloworld.c" Example

A simple Hello World application can demonstrate some of the debugger's
basic features. Create a new file named 'helloworld.c' in a working
directory. Add the following code to it:

``` 
   #include 
   int main( int argc, char *argv[] )
   {
     printf(&quot;Hello World!\n&quot;);
     for (; argc; argc-- )
     {
        fprintf(stderr, &quot;argv[%d] = %s\n&quot;, argc, argv[argc]);
     }
     return 0;
   }
```

To prepare the "helloworld.c", use the following command line

``` 
   icc -debug -O0 helloworld.c -o helloworld
```

To start the idb debugger, enter the following command in a shell:

``` 
   idb
```

and the debugger GUI front-end starts running.

## Open Executable in the Debugger

To open the executable once inside the debugger:

1.  In the debugger, select File \> Open Executable.
2.  Click the Browse button, navigate to your working directory and
    select the helloworld executable file.
3.  Click OK.

The debugger opens helloworld.

To open the executable file using the command line, enter the following
command:

``` 
 (idb) file helloworld
```

The debugger opens helloworld.

## Display the Source File

To display the source file using the GUI:

1.  Select View \> Source Files. The Source Files window appears,
    displaying a list of the project source files to be debugged.
2.  Double-click helloworld.c

The Source window displays the source code and sets the scope
appropriately.

To display the source file using the command line, enter the following
command:

``` 
 (idb) list main
```

The debugger displays the source code of the main function in
helloworld.

## Run the Application

To run helloworld:

1.  Using the GUI, select Run \> Run.
2.  Using the command line, enter 'run'.

## Breakpoints

To set a breakpoint:

1.  Enter the following command:
        (idb) break main
    A breakpoint is now set at function main().
2.  Enter run to run the application again.

The application should stop at the breakpoint you set.

To delete the breakpoint:

1.  List the IDs of all existing breakpoint by entering the following
    command:
        (idb) info breakpoints
    The debugger displays all existing breakpoints.
2.  Identify the ID of the breakpoint you want to delete. If you have
    not set any other breakpoints since starting the debugger, there is
    only one breakpoint, and its ID is 1.
3.  Delete the breakpoint by entering the following command:
        (idb) delete breakpoint 1
    You have deleted the breakpoint you set.
4.  Run the application again.

The application runs, and displays Hello World\! in the shell that
spawned the debugger, and the program exits.

## Exiting the Debugger

To exit the debugger:

1.  Select File \> Exit.
2.  Enter quit.

The debugger and all output files are closed.

## More Information

You can find more information once inside idb using the "help" command.
