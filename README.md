# Bookmark_url
http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
https://docs.google.com/document/d/1XXMvReO8-Awi1EZXAXS4PzDzdNvV6pGcuaF4Q9821Es/pub

Installing git on CentOS 5 using yum
====================================

Since you're using CentOS 5, the default *package manager* is `yum`, not `apt-get`. To install a program using it, you'd normally use the following command:
    
    $ sudo yum install <packagename>

However, when trying to install git this way, you'll encounter the following error on CentOS 5:


    $ sudo yum install git
    Setting up Install Process
    Parsing package install arguments
    No package git available.
    Nothing to do

This tells you that the package repositories that `yum` knows about don't contain the required rpms (RPM Package Manager files) to install `git`. This is presumably because CentOS 5 is based on RHEL 5, which was released in 2007, before `git` was considered a mature version control system. To get around this problem, we need to add additional repositories to the list that `yum` uses (We're going to add the RPMforge repository, as per [these instructions](http://wiki.centos.org/AdditionalResources/Repositories/RPMForge?action=show&amp;redirect=Repositories%2FRPMForge#head-b06dd43af4eb366c28879a551701b1b5e4aefccd)).


**This assumes you want the i386 packages. Test by running `uname -i`. If you want the x86_64 packages, replace all occurrences of i386 with x86_64 in the following commands**

First, download the `rpmforge-release` package:

    $ wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.i386.rpm

Next, verify and install the package:

    $ rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt
    $ rpm -K rpmforge-release-0.5.2-2.el5.rf.i386.rpm
    $ rpm -i rpmforge-release-0.5.2-2.el5.rf.i386.rpm

And now we should be able to install `git`:

    $ sudo yum install git-gui

`yum` will work out the dependancies, and ask you at relevant points if you want to proceed. Press <kbd>y</kbd> for Yes, and <kbd>n</kbd> or <kbd>return</kbd> for No.
