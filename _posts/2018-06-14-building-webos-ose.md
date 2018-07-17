---
ID: 150
post_title: BUILDING WEBOS OSE
author: iamadmin
post_excerpt: ""
layout: post
permalink: http://10.177.230.99/wordpress/?p=150
published: true
post_date: 2018-06-14 15:36:52
---
This page describes how to build the webOS Open Source Edition (OSE) image. Before you begin, ensure that your system meets the <a class="highlight" href="http://webosose.org/discover/setting/requirements/#build_system_requirements">Build System Requirements</a>.
<h2 id="repository">Repository <i class="fa fa-link fa-lg"></i></h2>
To build the image of webOS OSE, the <code>build-webos</code> repository is used.

The repository contains the top level code that aggregates the various <a class="highlight" href="http://openembedded.org/">OpenEmbedded</a> layers into a whole from which the webOS OSE image can be built.
<h2 id="images">Images <i class="fa fa-link fa-lg"></i></h2>
The following images can be built:
<ul>
 	<li><code>webos-image</code>: The production webOS OSE image without development tools.</li>
 	<li><code>webos-image-devel</code>: The image with various development tools added to <code>webos-image</code>, including GDB and strace (system call tracer).</li>
</ul>
<h2 id="cloning-the-repository">Cloning the Repository <i class="fa fa-link fa-lg"></i></h2>
Set up <code>build-webos</code> by cloning its Git repository:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ git clone https://github.com/webosose/build-webos.git</code></pre>
</div>
<h2 id="installing-the-required-tools">Installing the Required Tools <i class="fa fa-link fa-lg"></i></h2>
Before you can build, you need to install some tools. If you try to build without them, BitBake will fail a sanity check and tell you what’s missing, but not really how to get the missing pieces. On Ubuntu, you can force all of the missing pieces to be installed by entering:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ sudo scripts/prerequisites.sh</code></pre>
</div>
Also, the BitBake sanity check will issue a warning if you’re not running under Ubuntu 14.04 LTS 64-bit.
<h2 id="building">Building <i class="fa fa-link fa-lg"></i></h2>
<h3 id="configuring-the-build">Configuring the Build <i class="fa fa-link fa-lg"></i></h3>
To configure the build for Raspberry Pi 3 and to fetch the sources, type:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ ./mcf raspberrypi3</code></pre>
</div>
<h4 id="setting-the-parallelism-values">Setting the Parallelism Values <i class="fa fa-link fa-lg"></i></h4>
You can use <code>-p</code> and <code>-b</code> options to set the make and BitBake parallelism values. The <code>-p</code> and <code>-b</code> options correspond to <code>PARALLEL_MAKE</code> and <code>BB_NUMBER_THREADS</code> variables described in <a class="highlight" href="http://www.yoctoproject.org/docs/2.5/dev-manual/dev-manual.html#speeding-up-the-build">Yocto Project Development Tasks Manual</a>.

The default value for these options is 0, so the command above is equivalent to the following:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ ./mcf -p 0 -b 0 raspberrypi3</code></pre>
</div>
Using 0 as arguments to these options sets the make and BitBake parallelism values to the number of CPU cores found on your computer, which means the build process will use all CPU cores.

If you do not want to use all CPU cores on your computer, use different values as arguments to <code>-p</code> and <code>-b</code> options.
<h3 id="building-the-image">Building the Image <i class="fa fa-link fa-lg"></i></h3>
<h4 id="building-webos-image">Building webos-image <i class="fa fa-link fa-lg"></i></h4>
To kick off a full build of webOS OSE, enter the following:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ source oe-init-build-env
$ bitbake webos-image</code></pre>
</div>
Alternatively, you can enter:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ make webos-image</code></pre>
</div>
This may take in the neighborhood of two hours on multi-core workstation with a fast disk subsystem and lots of memory, or many more hours on a laptop with less memory and slower disks.
<div class="alert alert-info" role="alert">For more details about BitBake, refer to the <a class="highlight" href="https://www.yoctoproject.org/documentation/bitbake-user-manual-0">BitBake Manual</a>.</div>
<h4 id="building-webos-image-devel">Building webos-image-devel <i class="fa fa-link fa-lg"></i></h4>
To build a webOS OSE image that includes GDB and strace for debugging, enter the following:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ source oe-init-build-env
$ bitbake webos-image-devel</code></pre>
</div>
<div class="alert alert-info" role="alert">For details on setting up the environment to debug webOS OSE with GDB, see <a class="highlight" href="http://webosose.org/discover/setting/setting-gdb-debugging/">here</a>.</div>
<div class="alert alert-info" role="alert">For more information on how to use strace, refer to <a class="highlight" href="https://www.thegeekstuff.com/2011/11/strace-examples/">this article</a>.</div>
<h2 id="cleaning">Cleaning <i class="fa fa-link fa-lg"></i></h2>
To blow away the build artifacts and prepare to do the clean build, you can remove the build directory and recreate it by typing:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ rm -rf BUILD</code></pre>
</div>
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ ./mcf.status</code></pre>
</div>
What this retains are the caches of the downloaded source (under <code>./downloads</code>) and shared state (under <code>./sstate-cache</code>). These caches will save you a tremendous amount of time during development as they facilitate incremental builds, but can cause seemingly inexplicable behavior when corrupted. If you experience strangeness, use the command presented below to remove the shared state of suspicious components. In extreme cases, you may need to remove the entire shared state cache. See <a class="highlight" href="http://www.yoctoproject.org/docs/latest/poky-ref-manual/poky-ref-manual.html#shared-state-cache">here</a> for more information on it.
<h2 id="building-and-cleaning-individual-components">Building and Cleaning Individual Components <i class="fa fa-link fa-lg"></i></h2>
To build an individual component, enter:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ source oe-init-build-env
$ bitbake &lt;component-name&gt;</code></pre>
</div>
Alternatively, you can enter:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ make &lt;component-name&gt;</code></pre>
</div>
To clean a component’s build artifacts under BUILD, enter:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ source oe-init-build-env
$ bitbake -c clean &lt;component-name&gt;</code></pre>
</div>
To remove the shared state for a component as well as its build artifacts to ensure it gets rebuilt afresh from its source, enter:
<div class="highlight">
<pre><code class="language-bash" data-lang="bash">$ source oe-init-build-env
$ bitbake -c cleansstate &lt;component-name&gt;</code></pre>
</div>