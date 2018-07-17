---
ID: 146
post_title: REQUIREMENTS
author: iamadmin
post_excerpt: ""
layout: post
permalink: http://10.177.230.99/wordpress/?p=146
published: true
post_date: 2018-06-14 15:35:12
---
<p>Before you set up an environment for webOS Open Source Edition (OSE) development, make sure that you prepare the target device and systems that meet the following requirements.</p>
<div class="alert alert-info" role="alert">webOS OSE cannot be built directly on the target device. You must use a separate Linux desktop with Ubuntu 14.04 64-bit installed. For more details, refer to the <a class="highlight" href="http://webosose.org/discover/setting/requirements//#build_system_requirements">Build System Requirements</a>.</div>
<h2 id="target-device-requirements">Target Device Requirements <i class="fa fa-link fa-lg"></i></h2>
webOS OSE is optimized for <strong>Raspberry Pi 3</strong>. To test apps and components on Raspberry Pi 3, we recommend that you prepare the following set of hardware and peripherals.
<ul>
 	<li>Raspberry Pi 3</li>
 	<li>microSD card (8GB or larger) and microSD card reader device</li>
 	<li>HDMI-compliant monitor and cable</li>
 	<li>Input devices such as a keyboard and a mouse</li>
 	<li>Ethernet cable and internet connection</li>
</ul>
<h2 id="build-system-requirements">Build System Requirements <i class="fa fa-link fa-lg"></i></h2>
<p>To build webOS OSE image, you need a <strong>Linux</strong> machine. Building under Windows or Mac OS is not currently supported.<p>
<h3 id="operating-system">Operating System <i class="fa fa-link fa-lg"></i></h3>
Install <strong>Ubuntu 14.04 LTS 64-bit</strong>, which is the only build platform currently supported by webOS OSE.
<div class="alert alert-info" role="alert">We strongly recommend you NOT to use Linux virtual machine on Windows or Mac OS for building webOS OSE, as it may cause unexpected issues.</div>
<h3 id="hardware">Hardware <i class="fa fa-link fa-lg"></i></h3>
<table>
<thead>
<tr>
<th></th>
<th>MINIMUM REQUIREMENTS</th>
<th>RECOMMENDED</th>
</tr>
</thead>
<tbody>
<tr>
<td>CPU</td>
<td>Intel i5 dual-core with 4 threads</td>
<td>Intel i7 quad-core with 8 threads or higher</td>
</tr>
<tr>
<td>RAM</td>
<td>8 GB</td>
<td>16 GB or higher</td>
</tr>
<tr>
<td>Storage</td>
<td>HDD with 100 GB of free disk space</td>
<td>SSD with 100 GB of free disk space or more</td>
</tr>
</tbody>
</table>
<h3 id="software-tools">Software Tools <i class="fa fa-link fa-lg"></i></h3>
Before you start building webOS OSE, you need to install and set up the following tools.
<h4 id="git">Git <i class="fa fa-link fa-lg"></i></h4>
You need to <a class="highlight" href="https://help.github.com/articles/set-up-git">set up Git</a> in your build system.
<div class="alert alert-info" role="alert">Make sure that you follow “Connecting over SSH” in <a class="highlight" href="https://help.github.com/articles/set-up-git/#next-steps-authenticating-with-github-from-git">Authenticating with GitHub from Git</a>.</div>
<h4 id="python">Python <i class="fa fa-link fa-lg"></i></h4>
You need to install <a class="highlight" href="https://www.python.org/">Python</a> in your build system to proceed with the build process.
<h2 id="host-machine-requirements">Host Machine Requirements <i class="fa fa-link fa-lg"></i></h2>
On the host machine, you can flash the built image or use Command Line Interface (CLI) for further development processes. You can use Linux, Windows, or Mac OS for the host machine.
<div class="alert alert-info" role="alert">You can use the build system (Linux machine) as a host machine for further development processes.</div>
<h3 id="operating-systems">Operating Systems <i class="fa fa-link fa-lg"></i></h3>
Recommended version for each operating system are as follows:
<ul>
 	<li>Linux: Ubuntu 14.04 or later</li>
 	<li>Windows: Windows 7 or later</li>
 	<li>Mac OS: macOS 10.6 (Snow Leopard) or later</li>
</ul>
<h3 id="tools-for-enact-based-app-development">Tools for Enact-based App Development <i class="fa fa-link fa-lg"></i></h3>
To develop an app using Enact library, you will need to install specific version of Node.js and npm. For more detailed information, refer to <a class="highlight" href="http://enactjs.com/">enactjs.com</a>.