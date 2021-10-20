Time Machine Installation/De-installation Readme (Linux)

----------------------------------------------------
1. Time Machine System Requirements
----------------------------------------------------

  Time Machine is supported on the following UNIX platforms.

    AIX    HP-UX    Solaris    Linux

  Minimum disk space recommended:
  /tmp 70 MB (during installation only)
  /etc 65 MB

----------------------------------------------------
2. Obtaining Time Machine installation binaries
----------------------------------------------------

  An evaluation copy of Time Machine can be obtained via FTP

  From a UNIX shell login, connect to our FTP site (ftp.solution-soft.com).

	a) cd /tmp
	b) ftp ftp.solution-soft.com
	c) User name: anonymous
	d) passwd: use your e-mail address as the password
	e) Please type bin for binary
	f) cd /pub/tm
	g) Next traverse directory structure under /tm to the OS version you
	   want to download.
		Ex: cd linux/redhat/64bit (for Linux RedHat x86_64 system)
		(you'll get a compressed tarball for Linux RedHat x86_64 system)
		Ex: tm_linux_2.6.up_x86_64-12.7R4.tgz
	h) Get the release by typing "mget *"
	i) type bye to exit

----------------------------------------------------
3. Installing/De-installing Time Machine on Linux
----------------------------------------------------


Time Machine Linux Installation

Time Machine for Linux is made available as an RPM package and a shell script
packaged inside the compressed tarball. Expand the files to the directory.

For SuSE Linux:

tm_linux_suse12_3.12.up_x86_64-12.5-6.x86_64.rpm
ssstm_suse_install.sh

For other Linux:

tm_linux_2.6.up_x86_64-12.7R4.rpm
ssstm_install.sh

To install for SuSE Linux, from root:

   # ./ssstm_suse_install.sh tm_linux_suse12_3.12.up_x86_64-12.5-6.x86_64.rpm

To install for other Linux, from root:

   # ./ssstm_install.sh tm_linux_2.6.up_x86_64-12.7R4.rpm

NOTE: The rpm filename is an example. Actual filename downloaded from FTP site may be different.

NOTE: For non-SuSE Linux, Time Machine uses yum to add and then remove
      dependent packages during install so that you are not left with packages
      on the system that are not needed during runtime.
      For SuSE Linux, or if your organization does not use public repositories
      available for your specific Linux distribution, you will need to supply
      the dependent packages manually.

Re-installation of Time Machine

For non-SuSE Linux, Time Machine no longer needs to be uninstalled and
reinstalled when the loaded kernel changes. 

If the re-installation of Time Machine is needed for some other reasons,
(e.g., SuSE Linux) please follow the steps given below:

First, the system may need to be cleaned up first:

   a). Removing (de-install) previously installed Time Machine:

      # rpm -e [Time Machine installed package]

      Note: to find out the [Time Machine installed package], do:

      # rpm -qa | grep tm_linux

      The output of this command should be [Time Machine installed package]

   b). reinstall it:

To reinstall for SuSE Linux, from root:

   # ./ssstm_suse_install.sh tm_linux_suse12_3.12.up_x86_64-12.5-6.x86_64.rpm

To reinstall for other Linux, from root:

   # ./ssstm_install.sh tm_linux_2.6.up_x86_64-12.7R4.rpm

NOTE: The rpm filename is an example. Actual filename downloaded from FTP site may be different.

Should the yum repositories not be configured correctly, or for SuSE Linux,
the automated installation above may fail.
In that case, follow these instructions for a manual installation.

Linux Installation Prerequisite

To install Time Machine successfully on a Linux system, the system should have
had certain rpm packages pre-installed.  If some of them are missing from the
system, the installation will not be successful.  The following errors may be
displayed at the installation time for this reason:

insmod /etc/ssstm/lib/modules/2.6.18-164.2.1.el5/3s_tm.ko failed
error: %post(tm_linux-2.6.x-12.7-4.x86_64) scriptlet failed, exit status 1

In order to avoid this problem, please check the following:

   a). Double check if gcc package has been installed on the system:

   # rpm -qa | grep gcc

   Something like the following should be displayed:

   libgcc-4....
   gcc-4....


   b). Double check if kernel packages have been installed properly on the system:

   # rpm -qa | grep kernel

   Something like the following should be displayed:

   kernel-2.6.18-308.1.1.el5.x86_64
   kernel-headers-2.6.18-308.1.1.el5.x86_64
   kernel-devel-2.6.18-308.1.1.el5.x86_64

   Note that all the version numbers of the above packages should match exactly.
   ("2.6.18-308.1.1.el5" as shown in the above example), and the version number
   matchs the version number of the running kernel on the system.

   To see the version number of the running kernel on the system, use:

   # uname -r


----------------------------------------------------
4. Licensing Time Machine
----------------------------------------------------

To obtain the necessary license key(s) to run Time Machine, email
Solution-Soft with the following information:

As root, run "ssslicmgr -k", copy & paste the output and email the output to
support@Solution-soft.com.

Please also include the following contact information:
	your name
	company name
	email address
	phone number
	demo/extension/permanent key requested

After the key is successfully installed please email the resulting
number string to support@Solution-soft.com

You can also use Time Machine Floating License Server for licensing.
Please check with the administrator of the TM Floating License Server to see if
this option is available for your company. If this option is available, create
the file /opt/solutionsoft/timemachine/licserverhost and add a line with the
following information:

ipaddress:port:securitycode

Where ipaddress is the IP Address of the license server, where port is the TCP
port the license server listens on and where securitycode is a code chosen for
the organization determined by the license server administrator. EX:

     192.168.5.15:17777:ffbdaa


----------------------------------------------------
5. Contacting Support
----------------------------------------------------

NOTE: If you received any support code messages and cannot resolve the issue
yourself, please make a note of the support code(s) and contact us:
    
    Solution-Soft
    Phone: US 1+ 408 346 1414
    Email: support@solution-soft.com
    Web: www.solution-soft.com


----------------------------------------------------
6. SUPPLEMENTAL INFORMATION
----------------------------------------------------

The following sections describe setup or operations that may be needed to
be run for various operating systems depending on your environment

Allowing all Users to modify their own Virtual Clock (optional)

Depending on the security policy of your company, users can be allowed
to set their own virtual clocks with Time Machine. To allow users to set
their own virtual clocks, the system administrator will need to run
"tmuser_setup".

	RUN: % /etc/ssstm/tmuser_setup

----------------------------------------------------
7. NEW FEATURES
----------------------------------------------------

When using "tmuser" program to set the virtual clock for users,
a new "continue" option "-c" is introduced for the needs to set a virtual
clock that is relative to current active virtual time.

Without "-c" relative time calculation would be offset to current system
time.  With "-c" the calculation would offset to current active virtual
time.   "-c" would be ignored if no current active virtual clock or
"-x" absolute time is specified.

For example, if current system time is March 31, 2015 midnight and
there is an active virtual clock for user1 set one year ahead.
Then current virtual time for user1 is March 31, 2016.

tmuser -a -u user1 -y 2 -c would set the new virtual clock at March 31, 2018
tmuser -a -u user1 -y 2 would set the new virtual clock at March 31, 2017

The other example is to change the virtual clock speed and continue
ticking virtually from the current virtual time.

Let's say there is a virtual clock running at 2 time faster for user1
and the current virtual time March 31, 2015 1:30AM

tmuser -a -u user1 -s 4 -c would make the virtual clock running 4 times
faster and continue ticking from March 31, 2015 1:30AM

tmuser -a -u user1 -s 4 would make the virtual clock running 4 times
faster but start ticking from current system time.

----------------------------------------------------
For more detail information, please check the TM manual (tmmanual.txt).


