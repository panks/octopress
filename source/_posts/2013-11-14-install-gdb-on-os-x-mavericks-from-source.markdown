---
layout: post
title: "Install GDB on OS X Mavericks from source"
date: 2013-11-14 18:02
comments: true
categories: 
---

![Mavericks logo](/images/posts/Mavericks-logo.png)
With Mavericks Update, Apple has replaced GDB by LLDB, which is a part of the [LLVM](http://llvm.org/) suit.

It might have been a good move on Apple's side as it includes tons of new features and is also catching up with gdb on the run-time performance part (you can read more about it [here](http://lldb.llvm.org/tutorial.html)).
But I needed GCC and GDB for one of my projects and so here goes a post about it.

##Installation
You can get GCC by installing **Command-line-tools** package in OS X.

If you hit `gcc` in terminal it will prompt you for installing command line tool package, you can also fetch it directly from Apple dev download section [https://developer.apple.com/downloads/](https://developer.apple.com/downloads/).

But that comes with LLDB as the debugger, unlike previous releases of OS X (till Mountain Lion) which included GDB too.
<!--more-->

You can install GDB using Homebrew or Macports (see below for instructions), but here I'll be covering up how to install it from source in detail.
###Homebrew
    brew install homebrew/dupes/gdb

###Macports
    sudo port install gdb

and `sudo ggdb` will launch gdb

###From Source

####Fetch the source 

Fetch the gdb source from the gnu ftp [ftp://ftp.gnu.org/gnu/gdb/](ftp://ftp.gnu.org/gnu/gdb/). I used version [7.6.1](ftp://ftp.gnu.org/gnu/gdb/gdb-7.6.1.tar.gz) (latest at the time of writting this post).

####Compile it
While building release after 7.0 on Mac you might get errors which should have been "warning: format not a string literal and no format arguments" warnings. To avoid this we will configure along with `--disable-intl` flag. 

    ./configure --disable-intl

Furthur we will modify the generated Makefile to supress the errors

Change line 383 (in version 7.6.1) in Makefile to

    CFLAGS = -g -O2 -Wno-string-plus-int

Compile the source
    make

and Install it

    sudo make install


##Setting it up

Now if you try to debug using `gdb` you would get the following error

    Unable to find Mach task port for process-id 28885: (os/kern) failure (0x5).
     (please check gdb is codesigned - see taskgated(8))

This is because to run a process under a debugger, debugger needs to have complete access over the process, which Darwin kernel will not allow by default, because it can be used in malicious ways.

So to allow gdb to control another process we need to sign it with any system-trusted code signing authority.
For that you need to generate a certificate.

###Generate Certificate for signing

Launch Keychain Access application : **Launchpad > Others > Keychain Access**

![Keychain Access Window](/images/posts/keychainaccess.png)

Open menu **Keychain Access > Certificate Assistant > Create a Certificate...**

![Keychain Access Window](/images/posts/keychainaccess2.png)

Choose some name for the certificate (gdbc here), 

Identity Type: `Self Signed Root`

Certificate Type: `Code Signing`

and check the `Let me override defaults` checkbox. 

Keep continuing with default values untill you get the dialog box where you need to specify the location for the certificate, set the Keychain to `System`

![Keychain Access Window](/images/posts/keychainaccess3.png)

After the certificate is created you can see it in under **System** keychains.

Select **Get Info** from the context menu and in the dialoge box that appears expand **Trust** and set **Code Signing** to `Always Trust`.

Now quit Keychain Access application and restart `taskgated` process by killing it
    killall taskgated


Now to sign the certificate you can run

    codesign -fs gdbc /usr/local/bin/gdb

but it will ask for an administrative username and it's password. You need to enable `root` user to do so.


###Enable Root user


* From the Apple menu choose **System Preferences...**.
* From System Preferences window choose **Users & Groups**.

![Keychain Access Window](/images/posts/eru.png)

* Click the lock and authenticate as an administrator account.
* Click **Login Options...**.
* Click the **Join...** button at the bottom right.
* Click the **Open Directory Utility...** button.

![Keychain Access Window](/images/posts/eru2.png)

* Click the lock in the Directory Utility window and authenticate as an administrator account.
* Choose **Enable Root User** from the Edit menu.

![Keychain Access Window](/images/posts/eru3.png)

* Enter the root password you wish to use in both the Password and Verify fields, then click OK.


##The End
Now just run the following command to sign the certificate, enter username as `root` and it's password and you are done.

    codesign -fs gdbc /usr/local/bin/gdb

Live long and prosper





