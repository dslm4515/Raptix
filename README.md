# Raptix
An open-source operating system (OS) running a Linux kernel with a custom filesystem hierarchy.

The focus of this project is to develop an operating system using an alterntive to the Filesystem Hierarchy Standard (FHS). This was inspired by "build notes" of [qLinux](https://qlinux.qware.org/doku.php/0verview). To speed up the build, [mussel](https://github.com/firasuke/mussel) tool chain will be used to initiate the building process.

## S T A T U S : Underdevelopment (no finished bootable build yet)
Tested architectures:
<ul>
<li>x86-64: In progress, on Glibc host</li>
<li>i686: pending </li>
<li>aarm64: pending </li>
</ul>

### OS Specifications
<ul>
<li>Kernel: [Linux](kernel.org)</li>
<li>Default Compiler: GCC</li>
<li>C Runtime Library: [Musl](https://musl.libc.org/)</li>
<li>Init/Boot System: Custom implementation of [S6+S6-rc](https://skarnet.org/software/s6)</li>
<li>Device Manager: Eudev</li>
<li>Default shell: [Dash](http://gondor.apana.org.au/~herbert/dash) </li>
</ul>

## Custom Filesystem Hierarchy Goals
The filesystem hierarchy used by Raptix is defined in /FHS of this repo.
<ul>
  <li>Establish a functional filesystem hierarchy from the ground up. </li>
  <li>The /system directory will contain the 'base OS'. This will be a minimal system that can boot and launch a shell. </li>
  <li>The /apps directory will contain all the software _not required_ for boot. </li>
</ul>

## (Current) Issues
<ul>
<li> [ ] /etc still expected by bash to resolve users. "I have no name!" prompt.</li>
<li> [ ] /dev still expected to be present instead of /system/dev. Lots of scripts (i.e. configure of autotools) expect /dev/null. </li>
<li> [ ] Lots of software look for /apps/include instead of /apps/inc...I might just stick with /apps/include </li>
<li> [ ] GCC still expects /usr/include instead of /apps/inc or /apps/include. </li>
<li> [ ] "unknown terminal type." when clearing terminal. /system/data/terminfo is a "NetBSD Constant Database" instead of a directory of of files containing terminal definitions. </li>
<li> [ ] Musl libc wont compile in chroot. Make complains that "/bin/sh" does not exist. Yet executing 'failing' commands execute fine... just not by `make`.</li>
</ul>

## Build Method
<ol>
<li>Build mussel </li>
<li>Use mussel to build enough software to chroot. </li>
<li>Chroot and build the final system. </li>
</ol>

## Requirements (to run mussel & build Raptix)
The following software should be installed. The first 25 can be checked via `./check.sh` in the top-level of the mussel repo.
Listed versions are the minimum version per LFS-11.2.x ... otherwise, use the latest versions available per your distro.

<ul>
<li>Bash 3.2</li>
<li>bc</li>
<li>binutils 2.13.1</li>
<li>bison 2.7</li>
<li>bzip2</li>
<li>ccache</li>
<li>coreutils 6.9</li>
<li>diffutils 2.8.1 </li>
<li>findutils 4.2.31</li>
<li>gawk 4.0.1</li>
<li>GCC(C & C++ support) 4.8</li>
<li>git</li>
<li>glibc/musl</li>
<li>grep 2.5.1a</li>
<li>gzip 1.3.12</li>
<li>linux kernel 3.2</li>
<li>lzip</li>
<li>m4 1.4.10</li>
<li>make 3.8</li>
<li>patch 2.5.4 </li>
<li>perl 5.8.8</li>
<li>rsync</li>
<li>sed 4.1.5 </li>
<li>tar 1.22</li>
<li>texinfo 4.7</li>
<li>wget/cURL</li>
<li>xz 5.0.0 </li>
<li>zstd</li>
</ul>
