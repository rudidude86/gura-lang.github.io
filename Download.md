---
layout: default
lang: en
title: Download
---
{% assign gura_version = '0.4.2' %}
{% assign gura_download_id = '60652' %}

Download
--------

### Packages

<table>
<tr>
<td>Windows Installer</td>
<td><a href="https://sourceforge.jp/projects/gura/downloads/{{ gura_download_id }}/gura-{{ gura_version }}-win32.msi/" class="link">gura-{{ gura_version }}-win32.msi</a></td>
</tr>
<tr>
<tr>
<td>Windows Binary</td>
<td><a href="https://sourceforge.jp/projects/gura/downloads/{{ gura_download_id }}/gura-{{ gura_version }}-win32.zip/" class="link">gura-{{ gura_version }}-win32.zip</a></td>
</tr>
<tr>
<td>Sorce Package</td>
<td><a href="https://sourceforge.jp/projects/gura/downloads/{{ gura_download_id }}/gura-{{ gura_version }}-src.tar.gz/" class="link">gura-{{ gura_version }}-src.tar.gz</a></td>
</tr>
<!--
<tr>
<td style="padding-top: 3em">
<a href="http://www.softpedia.com/progClean/Gura-Clean-220177.html">
<img src="images/softpedia_free_award_f.gif" border="0" alt="100% FREE award granted by Softpedia" /></a></td>
</tr>
-->
</table>

### Install into Windows

Just launch the installer
[gura-{{ gura_version }}-win32.msi](http://sourceforge.jp/projects/gura/downloads/{{ gura_download_id }}/gura-{{ gura_version }}-win32.msi/),
which will install necessary files and register file extensions `.gura`, `.guraw`, `.gurc` and `.gurcw` as executable ones.

### Install into Linux

In default configuration, Ubuntu and Fedora do not include C++ compilers and readline library.
Install them as follows before building Gura.

For Ubuntu:

    $ sudo apt-get install g++ libreadline5-dev

For Fedora:

    # yum install gcc gcc-c++ readline-devel

Download a source package
[gura-{{ gura_version }}.tar.gz](http://sourceforge.jp/projects/gura/downloads/{{ gura_download_id }}/gura-{{ gura_version }}.tar.gz/)
and follow the steps below to build and install Gura executables.

    $ tar xvfz gura-{{ gura_version }}.tar.gz
    $ cd gura-{{ gura_version }}
    $ mkdir build
    $ cd build
    $ ../configure
    $ make
    $ sudo make install
    $ sudo ldconfig     # for the first install

After that, follow the steps below to build and install Gura module files.

    $ ./build-modules
    $ sudo ./build-modules install

If you see any error messages, your system may not have been installed
with packages necessary to build the modules.
Install them and try building modules again.
