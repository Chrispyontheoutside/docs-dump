# dos2unix

dos2unix is a DOS/MAC to UNIX text file format converter. It is used to
convert files created or edited within a Windows/DOS or Mac environment
to a format acceptable for usage within UNIX systems.

The most common usage on TAMU HPRC clusters is to remove the hidden
Windows/DOS-specific characters contained within files (input, scripts,
...) that need to be parsed by some program or interpreter.

# Usage

To use dos2unix on a file named "my\_job\_script.sh":

` dos2unix my_job_script.sh`

**Note:** This tool must be used every time a program is edited within a
DOS environment. If you transfer a file to your local Windows computer
and edit it, but sure to use dos2unix again.

# Common causes

The two most common ways of introducing hidden characters:

1\. Using a Windows editor such as Notepad to edit your job files and
then copying to the HPRC clusters.

2\. Copying from a webpage or pdf file and pasting into your file
editor.

One way to check for hidden characters is to use the file command

`file my_job_script.sh`

Which may output the following indicating that you need to run dos2unix:

***ASCII English text, with CRLF line terminators***

If you see the following input then you should check again using a
second method.

***Bourne-Again shell script text executable***

A second way to check your file for hidden characters is to use the -v
option of the cat command

`cat -v my_job_script.sh`

Example 'cat -v' output showing hidden Ctrl+M characters at the end of
each line:

    #!/bin/bash^M
    ^M
    echo 'Hello World!'^M
    ^M

# Other types of hidden character

Correcting other types of hidden characters.

If you do 'cat my\_file.txt' and you see -2 (for example) and then you
do 'cat -v my\_file.txt' and see -2M-BM- then to convert the -2M-BM- to
-2 do the following:

If the results of 'file my\_file.txt' is of type

`UTF-8 Unicode text`

then do the following to convert the hidden characters and file type:

`cat my_file.txt > tmpfile`  
`iconv --from-code UTF-8 --to-code US-ASCII -c tmpfile > my_file.txt`
