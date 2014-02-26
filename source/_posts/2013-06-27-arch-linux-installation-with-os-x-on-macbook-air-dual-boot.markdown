---
layout: post
title: "Arch Linux Installation with OS X on Macbook Air (Dual Boot)"
date: 2013-06-27 12:59
comments: true
categories: [arch, linux, macbook, os x]
---
<center><img class="noborder" src="/images/posts/arch-apple_logo.png"></center>   

<p>Second day and finally now I can Dual boot my Macbook Air with <a href="https://www.archlinux.org">Arch Linux</a> and OS X (Mountain lion). Moments of happiness :D
If you are a regular Windows user the rest of the article would probably be of no use (also boring may be) to you, so I recommend you check out my other posts.</p>

<p>Phew.. So with Windows fan gone, lets go on to the next level, if you have been a Linux user for a while using Linux in a virtual machine or one of those <a href="http://www.ubuntu.com/about/about-ubuntu/derivatives">[<strong>fillAnyThingHere</strong>]untus</a> then you must be wondering why I wrote this post, as Linux installation unlike in 90s is pretty straight forward nowadays.</p>

<!--more-->


<p>So just to put some light, I was using Ubuntu(and it&#8217;s variants) since last few years, but as they started adding lots and lots of bells and whistles to it, just to attracted the newly migrated (Windows) users, it turned into an ugly OS which takes few seconds just to open the unity launcher(or whatever fancy name they gave it).</p>

<p>Check out this video on <a href="http://www.youtube.com/watch?v=Sh-cnaJoGCw">Why Linux (read Ubuntu) Sucks</a>, just for fun.</p>

<p>One more reason as to why I got stuck to these -untus was because we have a clone of Ubuntu&#8217;s repository in our local server at my college so installing anything was just a matter of seconds. Getting irritated (read Saturated if you are a -untu user) I finally decided to make a switch to Arch Linux. Which is a bare bone GNU/Linux OS which come with minimal set of packages and you add everything on your own whatever you wish to, a true DIY OS. Arch FTW! :D</p>


<p><del>But there was cost to it, once I made the switch I would be accessing package repositories at my internet speed (which is usually pathetic in my college),</del> (My college got Arch repo mirror finally, <a href="ftp://ftp.iitm.ac.in/archlinux">ftp://ftp.iitm.ac.in/archlinux</a>) so I kept procrastinating it, but finally while my internship at Microsoft India (writing this post from my cabin right now) I got a good internet bandwidth and finally made the switch.</p>

<p>Unlike those -untus the process of installing Arch Linux (I&#8217;m talking about Dual boot here, not just Arch on your entire hard disk) on Macbook Air is not just a &#8216;Press Next&#8217; process. You have to configure everything on your own starting from hard disk partition and type to your networking and even bootloader.
It took me two days to get it the way I wanted. So I thought I would document it down for the <a href="http://xkcd.com/979/">people from the future</a>.</p>

<p>Before I start I would like to point it out that <a href="https://wiki.archlinux.org/index.php/Beginners'_Guide">Arch Linux&#8217;s wiki</a> is one of the best documentations out there, though some people might argue that Gentoo has the best documentation, to which I won&#8217;t disagree. So read it up, have it at your side while installation, it&#8217;s THE Bible.</p>

<h2>Prepare the USB for booting</h2>

<ul>
<li><a href="https://www.archlinux.org/download/">Download</a> the latest ISO of Arch Linux</li>
<li>Make a bootable USB of Arch linux while you are in your OS X using <strong>dd</strong></li>
</ul>


<p><code>'dd if==&lt;path to .iso file&gt; of==/dev/&lt;yourdevice&gt; bs==1M'</code></p>

<p>(You can find your device Id by using <strong>diskutil</strong> type <code>diskutil list</code> in your OS X terminal)</p>

<p>Plug in your USB key and hold &#8216;alt/option&#8217; button while your system boots up, choose the USB to boot from.</p>

<h2>Partitioning</h2>

<p>Use <strong>cgdisk</strong></p>

<p>When the system is up and running. open cgdisk.</p>

<p><code>cgdisk /dev/sda</code></p>

<p>It would list you existing partion, don&#8217;t mess up with the Mac partition (there would be 3, normally) just use the free space and create 4 new partition (You can create more, I used same partion for root and home and had a swap partition).</p>

<p>Press down arrow key to select the free space and create new partitions, leave a free space of at least 128MB after Mac partitions before making the first partition.

Make the following 4 partitions:</p>

<pre><code>Size            Partition Type          Partition Name

128 MB          Apple HFS+              Boot Loader
256 MB          Linux filesystem        Boot
X MB            Linux Swap              Swap space
Rest of space   Linux filesystem        Root
</code></pre>

<p>Try to keep swap space (X) double the size of your physical memory (RAM).</p>

<h2>Keep the network ready</h2>

<p>As you are gonna download lot many packages you need to be online, so plugin your ethernet cable via adapter. Or you can do USB tethering from your smartphone. 

To connect to WiFi network run <code>wifi-menu</code>

</p>

<p>To check run:</p>

<p><code>ping google.com</code></p>

<h2>Format and mount partition</h2>

<pre><code>mkfs.ext4 /dev/sda5
mkswap /dev/sda6
mkfs.ext4 /dev/sda7
mount /dev/sda7 /mnt
mkdir /mnt/boot &amp;&amp; mount /dev/sda5 /mnt/boot
swapon /dev/sda6
</code></pre>

<h2>Installation</h2>

<pre><code>pacstrap /mnt base base-devel
genfstab -p /mnt &gt;&gt; /mnt/etc/fstab
</code></pre>

<p>[<strong>VERY IMP</strong>]
If your hard disk in SSD the change your fstab file parameters, open your fstab file <code>nano /mnt/etc/fstab</code> and make changes in it as below:</p>

<pre><code>/dev/sda5      /boot  ext2  defaults,relatime,stripe=4    0 2
/dev/sda7        /      ext4  defaults,noatime,discard,data=writeback   0 1
</code></pre>

<h2>Configure system</h2>

<pre><code>arch-chroot /mnt /bin/bash 
echo archer &gt; /etc/hostname     #Replace archer by whatever hostname you want to use
ln -s /usr/share/zoneinfo/Asia/Calcutta /etc/localtime 
hwclock --systohc --utc 
useradd -m -g users -G wheel -s /bin/bash myusername &amp;&amp; passwd mypassword   #Replace myusername and mypassword
sudo pacman -S sudo
</code></pre>

<p>Give yourself sudo right:</p>

<pre><code>nano /etc/sudoers # uncomment wheel line
</code></pre>

<p>To set up your locale, run:</p>

<pre><code>sudo nano /etc/locale.gen
</code></pre>

<p>Uncomment the desired locals. For me this was:</p>

<p><code>en_US.UTF-8 UTF-8</code></p>

<p><code>en_CA.UTF-8 UTF-8</code></p>

<p>Generate these locales by running:</p>

<pre><code>locale-gen
echo LANG=en_US.UTF8 &gt; /etc/locale.conf
export LANG=en_US.UTF-8
</code></pre>

<p>Modify your <strong>/etc/mkinitcpio.conf</strong> file to insert <code>keyboard</code> after <code>autodetect</code> in the <strong>HOOK</strong> section.
Then run:</p>

<pre><code>mkinitcpio -p linux
</code></pre>

<h2>Here comes the Bootloader</h2>

<p>This is the trickiest part, so don&#8217;t go anywhere.</p>

<p>What we will be doing is to boot using OS X native EFI boot loader, so install <strong>grub-efi-x86_64</strong></p>

<pre><code>pacman -S grub-efi-x86_64
</code></pre>

<p>change <strong>/etc/default/grub</strong> to look like</p>

<pre><code>GRUB_CMDLINE_LINUX_DEFAULT="quiet rootflags=data=writeback"</code></pre>

<p>Now generate <strong>boot.efi</strong> with GRUB</p>

<pre><code>grub-mkconfig -o boot/grub/grub.cfg
grub-mkstandalone -o boot.efi -d usr/lib/grub/x86_64-efi -O x86_64-efi -C xz boot/grub/grub.cfg</code></pre>

<p>Now <strong>boot.efi</strong> would be present in the current directly (or somewhere else if you changed the path in the command above), copy it somewhere.</p>

<p>How?</p>

<p>You can mount your USB and copy to it:</p>

<pre><code>mkdir /mnt/usbdisk &amp;&amp; mount /dev/sdb /mnt/usbdisk 
cp boot.efi /mnt/usbdisk/
</code></pre>

<p>Or you can SCP it to some other computer (for SSH you need to install <strong>openssh</strong> package).</p>

If you only have WiFi at your disposal and don't have an ethernet then you might wanna install the following packages before rebooting for the WiFi to work on reboot:

    yum install iw wireless_tools wpa_supplicant dialog

also install `networkmanager` and enable it using `NetworkManager.service`. Read [Arch wiki](https://wiki.archlinux.org/index.php/NetworkManager) for more info.

<h2>Reboot (Back to the Mac world)</h2>

<ul>
<li>exit chroot: <code>exit</code></li>
<li>Reboot your system <code>sudo reboot</code></li>
<li>Launch <strong>Disk Utility</strong></li>
<li>Format the partition made for boot (<strong>/dev/sda4</strong>), using Max OS X(Journaled) filesystem.</li>
<li><p>Create the following the directories and file in /dev/sda4:</p>

<pre><code>  |___mach_kernel
  |___System
              |
              |___Library
                      |
                      |___CoreServices
                          |
                          |___SystemVersion.plist
                          |___boot.efi
</code></pre></li>
</ul>


<p>Commands for more clarity:</p>

<pre><code>cd /Volumes/disk0s4
mkdir System mach_kernel
cd System
mkdir Library
cd Library
mkdir CoreServices
cd CoreServices
touch SystemVersion.plist
</code></pre>

<p>Copy the <strong>boot.efi</strong> generated while installation to <strong>CoreServices</strong> directory.
and paste the following in <strong>SystemVersion.plist</strong></p>

<pre><code>&lt;xml version="1.0" encoding="utf-8"?&gt;
&lt;plist version="1.0"&gt;
&lt;dict&gt;
    &lt;key&gt;ProductBuildVersion&lt;/key&gt;
    &lt;string&gt;&lt;/string&gt;
    &lt;key&gt;ProductName&lt;/key&gt;
    &lt;string&gt;Linux&lt;/string&gt;
    &lt;key&gt;ProductVersion&lt;/key&gt;
    &lt;string&gt;Arch Linux&lt;/string&gt;
&lt;/dict&gt;
&lt;/plist&gt;
</code></pre>

<p>and now <strong>bless</strong> this partition to make it bootable</p>

<pre><code>sudo bless --device /dev/disk0s4 --setBoot
</code></pre>

<p>Now you are all set, you can reboot and hold &#8216;alt/option&#8217; key and choose <strong>disk0s4</strong> to boot from to boot into Arch Linux.</p>

<h2>Post Installtion</h2>

<h3>Xorg</h3>

<p>Install Xorg server</p>

<pre><code>pacman -S xorg xf86-input-synaptics acpid
systemctl enable acpid
</code></pre>

<h3>Network</h3>

<ul>
<li><p>Use <code>iwconfig</code> to check the ethernet and run
<code>systemctl start dhcpcd.service@eth0</code> #or whatever your ethernet name is</p></li>
<li><p>You can use <code>wifi-menu</code> to connect to Wi-Fi Networks</p></li>
</ul>


<h3>Sound</h3>

<ul>
<li><p>Install <strong>ALSA</strong></p>

<p> <code>pacman -S alsa-utils</code></p></li>
<li><p>Unmute the master channel</p>

<p> <code>amixer sset Master unmute</code></p></li>
</ul>


<h3>Screen Backlight</h3>

<p>Works OTB</p>

<h3>Keyboard Backlight</h3>

<p>You can control by echoing values to</p>

<p><strong>/sys/devices/platform/applesmc.768/leds/smc\:\:kbd_backlight/brightness</strong></p>

<pre><code>echo 40 &gt; /sys/devices/platform/applesmc.768/leds/smc\:\:kbd_backlight/brightness
</code></pre>

<h3>GUI</h3>

<p>There are lot many options for it, some might prefer living without it, some might go for something light, like <a href="https://wiki.archlinux.org/index.php/Awesome">awesome</a> or <a href="https://wiki.archlinux.org/index.php/Enlightenment">enlightenment</a>. But as of now I&#8217;m mentoring a student under <a href="http://www.google-melange.com/">GSoC</a> for a project which is in <a href="http://www.digikam.org">digiKam</a> so I prefered going for <a href="http://www.kde.org/">KDE</a>.</p>

<p>For minimal install, install <strong>kdebase</strong> for full install of all the basic KDE packages install <strong>kde</strong></p>

<pre><code>pacman -S kdebase
</code></pre>

<p>For launching KDE:</p>

<ul>
<li><p>Using <strong>xinitrc</strong></p>

<ul>
<li>Add <code>exec startkde</code> to <strong>~/.xinitrc</strong></li>
<li>After log-in run <code>startx</code> to launch KDE GUI</li>
</ul>
</li>
<li><p>Using KDM</p>

<ul>
<li>Install <strong>kdm</strong></li>
<li>Enable it <code>systemctl start kdm.service</code>, from next start  you would get a GUI asking for your password to login</li>
</ul>
</li>
</ul>


<h3>rEFInd</h3>

<p>If you find this whole business of holding &#8216;alt/option&#8217; key for few seconds on system start to choose OS irritation, then you can install <a href="http://www.rodsbooks.com/refind/">rEFInd</a> it would present you with a nice GUI on system start where you can choose which OS to boot.</p>

<h2>Install Application</h2>

<p>You can install any package using <strong>pacman</strong></p>

<pre><code>pacman -S &lt;package name&gt;
</code></pre>

<p>You can go <a href="https://wiki.archlinux.org/index.php/List_of_Applications">here</a> and check the list of Application which you might wanna use/install.</p>

<p>Well, so that&#8217;s all about it.
