---
ID: 152
post_title: FLASH WEBOS OSE
author: iamadmin
post_excerpt: ""
layout: post
permalink: http://10.177.230.99/wordpress/?p=152
published: true
post_date: 2018-06-14 15:37:24
---
This page provides details for flashing the webOS Open Source Edition (OSE) image to a microSD card. In addition, this page describes how to verify the flashed image on the target device.

<em>This paragraph has been inserted for test.</em>
<h2 id="prerequisites">Prerequisites <i class="fa fa-link fa-lg"></i></h2>
Before you begin flashing the webOS OSE image, make sure you have completed the following:
<ul>
 	<li>You must build the webOS OSE image on a Linux machine. For more information, see <a class="highlight" href="http://webosose.org/discover/setting/building-webos-ose/">here</a>.
<ul>
 	<li>To flash the image from Windows or Mac OS, you must download the built image from the Linux machine to the host machine.</li>
</ul>
</li>
 	<li>You must insert a microSD card in the microSD card reader device connected to the host machine.</li>
 	<li>This list item has been inserted for test.</li>
</ul>
<h2 id="flashing-the-image">Flashing the Image <i class="fa fa-link fa-lg"></i></h2>
This section describes how to flash the webOS OSE image (.rpi-sdimg) to a microSD card, for each host operating system.
<h3 id="windows">Windows <i class="fa fa-link fa-lg"></i></h3>
Flash the image using <a class="highlight" href="https://sourceforge.net/projects/win32diskimager/">Win32DiskImager</a>.
<h3 id="linux">Linux <i class="fa fa-link fa-lg"></i></h3>
First, change directory to where the image is located.
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ cd &lt;path where the image is located&gt;</code></pre>
</div>
Check the device name of the microSD card using the following command.
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ sudo fdisk -l</code></pre>
</div>
Run the commands as below to flash the image to the microSD card.
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ sudo umount /dev/sdXn
$ sudo dd bs=4M if=./**.rpi-sdimg of=/dev/sdX
$ sudo umount /dev/sdXn</code></pre>
</div>
<ul>
 	<li><code>sdXn</code> denotes the device name of the microSD card, where <code>n</code> is a number suffix.</li>
 	<li>For <code>dd</code> command, you must pass <code>sdX</code> (without the suffix number) as a destination parameter. This indicates the mass storage device, not the partition.</li>
</ul>
<div class="alert alert-info" role="alert">After you run the <code>dd</code> command, the shell prompt will not display any message until the job is finished. Even if there is no message, you need to wait until the copying process is complete. For more information on <code>dd</code> command, see <a class="highlight" href="https://en.wikipedia.org/wiki/Dd_(Unix)">here</a>.</div>
<h4 id="flashing-command-example-for-linux">Flashing Command Example for Linux <i class="fa fa-link fa-lg"></i></h4>
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ sudo umount /dev/sdb1
$ sudo dd bs=4M if=./webos-image-raspberrypi3.rootfs.rpi-sdimg of=/dev/sdb
$ sudo umount /dev/sdb1</code></pre>
</div>
<h3 id="mac-os">Mac OS <i class="fa fa-link fa-lg"></i></h3>
First, change directory to where the image is located.
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ cd &lt;path where the image is located&gt;</code></pre>
</div>
Check the device name of the microSD card using the following command.
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ diskutil list</code></pre>
</div>
Run the commands as below to flash the image to the microSD card.
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ sudo diskutil umountDisk /dev/diskn
$ sudo dd bs=4M if=./**.rpi-sdimg of=/dev/rdiskn
$ sudo diskutil umountDisk /dev/diskn</code></pre>
</div>
<ul>
 	<li><code>diskn</code> is the device name of the microSD card, where <code>n</code> is a number suffix.</li>
 	<li>For <code>dd</code> command, you need to pass <code>rdiskn</code> as a destination parameter to speed up the copying process.</li>
</ul>
<div class="alert alert-info" role="alert">After you run the <code>dd</code> command, the shell prompt will not display any message until the job is finished. Even if there is no message, you need to wait until the copying process is complete. For more information on <code>dd</code> command, see <a class="highlight" href="https://en.wikipedia.org/wiki/Dd_(Unix)">here</a>.</div>
<h4 id="flashing-command-example-for-mac-os">Flashing Command Example for Mac OS <i class="fa fa-link fa-lg"></i></h4>
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ sudo diskutil umountDisk /dev/disk2
$ sudo dd bs=4M if=./webos-image-raspberrypi3.rootfs.rpi-sdimg of=/dev/rdisk2
$ sudo diskutil umountDisk /dev/disk2</code></pre>
</div>
<h2 id="verifying-the-image">Verifying the Image <i class="fa fa-link fa-lg"></i></h2>
After you finish flashing the webOS OSE image to the microSD card, you can check how it works by taking the following steps:
<ol>
 	<li>First, eject the microSD card from the reader device and insert it in the target device, Raspberry Pi 3.</li>
 	<li>Connect the target device with peripherals.
<ul>
 	<li>First, connect the target device to a monitor through HDMI cable.</li>
 	<li>Second, plug a keyboard and a mouse into the USB ports of the target device.</li>
 	<li>Lastly, connect Ethernet cable to the target device.</li>
</ul>
</li>
 	<li>Set the input mode of the monitor to the port connected with the target device.</li>
 	<li>Plug the power cable in to the target device. The target device will boot up. On the monitor, a log message will appear for a short time. After that, a mouse cursor will show up.</li>
 	<li>Press F1 key on the keyboard, and you will see the Home Launcher UI popping up from the right side of the screen. Home Launcher should contain a list of pre-installed apps and an icon for Settings app, as shown in the figure below.</li>
</ol>
<div class="chevrons">
<div id="navigation"></div>
</div>