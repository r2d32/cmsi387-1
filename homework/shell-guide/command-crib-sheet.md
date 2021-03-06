# COMMAND CRIB SHEET

### 1. `traceroute`

The `traceroute` command is a program that shows you the route over the network between two systems, listing all the intermediate routers a connection must pass through to get to its destination. It can help you determine why your connections to a given server might be poor, and can often help you figure out where exactly the problem is.

Source: http://www.exit109.com/~jeremy/news/providers/traceroute.html

    frodosamoa:csmi387 andrewrkowalczyk$ traceroute google.com
    traceroute to google.com (74.125.236.132), 30 hops max, 60 byte packets
    1  220.224.141.129 (220.224.141.129)  89.174 ms  89.094 ms  89.054 ms
    2  115.255.239.65 (115.255.239.65)  109.037 ms  108.994 ms  108.963 ms
    3  124.124.251.245 (124.124.251.245)  108.937 ms  121.322 ms  121.300 ms
    4  * 115.255.239.45 (115.255.239.45)  113.754 ms  113.692 ms
    5  72.14.212.118 (72.14.212.118)  123.585 ms  123.558 ms  123.527 ms
    6  72.14.232.202 (72.14.232.202)  123.499 ms  123.475 ms  143.523 ms
    7  216.239.48.179 (216.239.48.179)  143.503 ms  95.106 ms  95.026 ms
    8  bom03s02-in-f4.1e100.net (74.125.236.132)  94.980 ms  104.989 ms  104.954 ms

This example was taken from http://www.thegeekstuff.com/2012/05/traceroute-examples/ due to LMU's network having interference with the `traceroute` command. This invocation was aiming to find all the "steps" in between my computer and google.com. Since the internet is a vast network of many connections, being able to trace where your connection goes is useful. The first line of the output shows the the target I am trying to reach, that target's IP address, the maximum number of hops, or connections, that will be allowed, and the size of the packets that will be sent. The next lines show each individual connection with the name of the system which is determined by the DNS, that individual system's IP address, and three different times. Each time specifes the time it took for a round trip to take for the packets that were sent. This will happen for eash step until the final destination is reached, as one can see the IP addresses in the first and last line of the output are the same.

### 2. `whoami`

The `whoami` command is used for printing the user name associated with the current effective user id. This is the same as id -un.

Source: http://linux.about.com/library/cmd/blcmdl1_whoami.htm
    
    frodosamoa:csmi387 andrewkowalczyk$ whoami
    andrewkowalczyk

This command asks the computer, in a quite literal sense, "Who am I?". The computer responds with the name of the current user.

### 3. `crontab`

The `crontab` file contains a list of Linux commands to be performed at specific times. A system administrator can use crontab as an automatic timer to trigger the initiation of important jobs.

Sources: http://linux.about.com/od/commands/l/blcmdl5_crontab.htm
http://www.thegeekstuff.com/2009/06/15-practical-crontab-examples/

    59 23 31 * * sudo rm -rf ~/.Trash
    30 7 3,9,20 1,6 * /usr/bin/newsyslog

Instead of a output of a program, I showed an example of the `crontab` file. The format for any `crontab` file is as follows: `MIN HOUR DOM MON DOW CMD`. Minute field, then hour field, day of month, day of the week, then the command. The ranges are as follows: `0-59, 0-23, 1-31, 1-12, 0-6`, then any command to be executed. In my file, one can see that the first line would empty the trash every month on the last day at 23:59. The second line of code would rotate logs at 7:30AM on the 3rd, 9th, and 20th day in the months of January and June.

### 4. `killall`

`killall` kills proceses by name.

     frodosamoa:csmi387 andrewkowalczyk$ defaults write com.apple.Finder AppleShowAllFiles TRUE
     frodosamoa:csmi387 andrewkowalczyk$ killall Finder

In this invocation, we are changing the defaults by allowing hidden files to be seen. In order for this change to occur, one needs to kill Finder, which is done by `killall`.

### 5. `uptime`

The command `uptime` prints out how long the system has been running.

Source: http://linux.about.com/library/cmd/blcmdl1_uptime.htm

    frodosamoa:csmi387 andrewkowalczyk$ uptime
    20:55  up 31 days, 12:15, 2 users, load averages: 1.10 1.00 1.01

This gives a one line display of the following information. The current time, how long the system has been running, how many users are currently logged on, and the system load averages for the past 1, 5, and 15 minutes.

### 6. `nslookup`

The command `nslookup` is used to question, or get more inforamtion about domain name servers. This command has an interactive mode and a non-interactive mode.

Source: http://linux.about.com/od/commands/l/blcmdl8_nslooku.htm

*6(a) Interactive*
    
    frodosamoa:csmi387 andrewkowalczyk$ nslookup
    > reddit.com
    Server:		157.242.6.5
    Address:	157.242.6.5#53

    Non-authoritative answer:
    Name:	reddit.com
    Address: 	67.148.47.33
    Name:	reddit.com
    Address: 	67.148.47.11
    > thoughtcatalog.com
    Server:	157.242.6.5
    Address:	157.242.6.5#53

    Non-authoritative answer:
    Name:	thoughtcatalog.com
    Address: 76.74.254.123
    Name:	thoughtcatalog.com
    Address: 76.74.254.120
    Name:	thoughtcatalog.com
    Address: 66.155.11.238
    Name:	thoughtcatalog.com
    Address: 72.233.2.58
    Name:	thoughtcatalog.com
    Address: 72.233.69.6
    Name:	thoughtcatalog.com
    Address: 66.155.9.238
    > exit 

*6(b) Non-interactive*

    frodosamoa:csmi387 andrewkowalczyk$ nslookup reddit.com
    Server:		157.242.6.5
    Address:	157.242.6.5#53

    Non-authoritative answer:
    Name:	reddit.com
    Address: 67.132.30.121
    Name:	reddit.com
    Address: 67.132.30.131

I provided an example of both the interactive mode and the non-interactive mode. In the first one, once `nslookup` is run with no arguments, this program can do a few things. In my invocation, I chose to ns lookup two websites, reddit.com and thoughtcatalog.com. The output shows the name of the server and it's IP address. Since these websites are pretty popular, they use multiple servers to handle incoming requests. In the second example, if "nslookup" is run with an argument after it, it will basically do that same as it would in its interactive mode.

### 7. `xargs`

The xargs utility reads space, tab, newline and end-of-file delimited strings from the standard input and executes utility with the strings as arguments.

Source: http://www.folkstalk.com/2012/07/xargs-command-examples-in-unix-linux.html

    frodosamoa:example andrewkowalczyk$ ls
    IMG_7821.jpg    IMG_7822.jpg	IMG_7823.jpg	IMG_7824.jpg
    frodosamoa:example andrewkowalczyk$ ls *.jpg | xargs rm
    frodosamoa:example andrewkowalczyk$ ls
    frodosamoa:example andrewkowalczyk$

This invocation removes all the files with ".tmp" suffix. As you can see, comparing the lists of the files in each directory one can see how this command works.

### 8. `tar`

On Unix platform, the `tar` command is the primary archiving utility. Understanding various tar command options will help you master the archive file manipulation. This command can create tar archives (with gzip and bzip compression), extract a single files or directories, view tar archive contents,  orvalidate the integrity of a tar archive.

Source: http://www.thegeekstuff.com/2010/04/unix-tar-command-examples/

    frodosamoa:csmi387 andrewkowalczyk$ tar cvf ASSINGMENT0124.tar ~/Desktop/Untitled.pdf
    tar: Removing leading '/' from member names
    a Users/andrewkowalczyk/Desktop/Untitled.pdf

In this invoking, I told the tar program to archive a file on my desktop called "Untitled.pdf" into my current directory and to name that archive file "ASSIGNMENT0124.tar". This archives the file making it into a "smaller" size.

### 9. `ssh-keygen`

The command `ssh-keygen` generates, manages and, converts authentication keys for ssh. It can create RSA keys for use by SSH protocol version 1 and RSA or DSA keys for use by SSH protocol version 2. The type of key to be generated can be specified with the -t option.

Source: http://www.thegeekstuff.com/2008/11/3-steps-to-perform-ssh-login-without-password-using-ssh-keygen-ssh-copy-id/#more-268

    frodosamoa:csmi387 andrewkowalczyk$ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/Users/andrewkowalczyk/.ssh/id_rsa): 
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in /Users/andrewkowalczyk/.ssh/id_rsa.
    Your public key has been saved in /Users/andrewkowalczyk/.ssh/id_rsa.pub.
    The key fingerprint is:
    2a:ac:70:53:46:84:a4:9d:4f:d6:d6:bf:30:07:ce:09 andrewkowalczyk@frodosamoa.local
    The key's randomart image is:
    +--[ RSA 2048]----+
    | ....            |
    | o.o . .         |
    |. o + E o        |
    |   = . + +       |
    |    +   S o      |
    |   +   . + .     |
    |. o o .   .      |
    | o o .           |
    |  .              |
    +-----------------+
    
In this invocation, I created a new ssh keygen in the `/Users/andrewkowalczyk/.ssh/id_rsa` file. I enter the passphrase to make the encrytion unique and once that and the public key has been saved, the command prints out the public key and a more visual representation of the keygen by making a randomart image representation. 

### 10. `which`

The `which` command takes a list of program names and looks for the files that run when these names are given as commands.

Source: http://unixhelp.ed.ac.uk/commanz/cmd5.1.html

    frodosamoa:csmi387 andrewkowalczyk$ which traceroute hexdump csh java
    /usr/sbin/traceroute
    /usr/bin/hexdump
    /bin/csh
    /usr/bin/java
    
In this invocation, I give `which` four different commands. In this case, they are `traceroute`, `hexdump`, `csh`, and `java`. It then prints out 4 lines, one for each argument and shows where the file is. If a certain command is not found, the command prints out nothing for that certain command.
