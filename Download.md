---
layout: default
lang: en
title: Download
---
{% assign gura_version = '0.5.2' %}

# {{ page.title }}


## Packages

<table>
<tr>
<td>Windows Installer</td>
<td><a href="https://github.com/gura-lang/gura/releases/download/v{{ gura_version }}/gura-{{ gura_version }}-win32.msi" class="link"
  onClick="_gaq.push(['_trackEvent','download','click','gura-{{ gura_version }}-win32.msi']);">gura-{{ gura_version }}-win32.msi</a></td>
</tr>
<tr>
<tr>
<td>Windows Binary</td>
<td><a href="https://github.com/gura-lang/gura/releases/download/v{{ gura_version }}/gura-{{ gura_version }}-win32.zip" class="link"
  onClick="_gaq.push(['_trackEvent','download','click','gura-{{ gura_version }}-win32.zip']);">gura-{{ gura_version }}-win32.zip</a></td>
</tr>
<tr>
<td>Sorce Package</td>
<td><a href="https://github.com/gura-lang/gura/releases/download/v{{ gura_version }}/gura-{{ gura_version }}-src.tar.gz" class="link"
  onClick="_gaq.push(['_trackEvent','download','click','gura-{{ gura_version }}-src.tar.gz']);">gura-{{ gura_version }}-src.tar.gz</a></td>
</tr>
<!--
<tr>
<td style="padding-top: 3em">
<a href="http://www.softpedia.com/progClean/Gura-Clean-220177.html">
<img src="images/softpedia_free_award_f.gif" border="0" alt="100% FREE award granted by Softpedia" /></a></td>
</tr>
-->
</table>


## Install into Windows

It has been confirmed that Gura runs on the following versions of Windows.

* Windows 7
* Windows 8.1

Launch the installer
<a href="https://github.com/gura-lang/gura/releases/download/v{{ gura_version }}/gura-{{ gura_version }}-win32.msi" class="link"
  onClick="_gaq.push(['_trackEvent','download','click','gura-{{ gura_version }}-win32.msi']);">gura-{{ gura_version }}-win32.msi</a>,
which will install necessary files and register file extensions `.gura`, `.guraw`, `.gurc` and `.gurcw` as executable ones.

If you don't want to modify registry, you can just expand ZIP file
<a href="https://github.com/gura-lang/gura/releases/download/v{{ gura_version }}/gura-{{ gura_version }}-win32.zip" class="link"
  onClick="_gaq.push(['_trackEvent','download','click','gura-{{ gura_version }}-win32.zip']);">gura-{{ gura_version }}-win32.zip</a>
  in some directory. Then modify PATH environment so that it includes `gura\bin-x86` directory.


## Install into Linux

It has been confirmed that Gura runs on the following distributions of Linux.

* Ubuntu 13.10
* Ubuntu 14.04
* Xubuntu 14.04
* lubuntu 14.04
* Fedora 20 (`wx` modules doesn't work well)

In default configuration, Ubuntu and Fedora do not include C++ compilers, cmake utility and readline library.
Install them as below before building Gura.

For Ubuntu:

    $ sudo apt-get install build-essential cmake libreadline-dev

For Fedora:

    # yum install gcc gcc-c++ make cmake readline-devel

Download a source package
<a href="https://github.com/gura-lang/gura/releases/download/v{{ gura_version }}/gura-{{ gura_version }}-src.tar.gz" class="link"
  onClick="_gaq.push(['_trackEvent','download','click','gura-{{ gura_version }}-src.tar.gz']);">gura-{{ gura_version }}-src.tar.gz</a>.
Then, follow the steps below to build Gura executables and modules.

    $ tar xvfz gura-{{ gura_version }}.tar.gz
    $ cd gura-{{ gura_version }}
    $ mkdir build
    $ cd build
    $ ../configure
    $ make
    $ sudo ./setup-guest
    $ ./build-modules

After that, follow the steps below to install them to the system.

    $ sudo make install
    $ sudo ldconfig     # only necessary for the first install
    $ sudo ./build-modules install
