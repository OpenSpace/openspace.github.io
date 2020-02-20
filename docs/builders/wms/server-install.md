---
title: Server Install
layout: default

grand_parent: Builders
parent: WMS
nav_order: 1
---

This wiki covers the steps required to get an OpenSpace WMS (Web Map Server) configured & running.  This serves MRF (Meta Raster Format) files.  Another name for this service is AHTSE (An Httpd/apache Tile-Serving Engine).
[This wiki](server-import) covers the steps involved in importing WMS dataset(s) so that the AHTSE can serve tiles from the set.  [This wiki](server-conversion) covers the steps involved in converting a raw raster image into the MRF format.

These instructions are specific to a Linux server install.

## Web Server Setup

Install the following software via the Operating System's package installer.
1. Apache2 web server (version 2.4.23 or higher is required).
1. Apache2 header files (this might be in the form of a **dev**elopment install apckage.
1. GDAL (version 2.2 or higher is recommended).

Install the five MRF modules (**mrf**, **receivef**, **sfim**, **reproject**, **convert**), which run as modules in the Apache web server.  For each module, it is necessary to download the source code, compile the module, and configure Apache to run the module.  The steps are similar for all modules, so instructions are given first for the **mod_mrf** module, and then any differing or specific information is provided for the others in subsequent sections.
**Note**: The mrf module depends on the **mod_receive** module, which has to be installed *first*.

## Add the _mod_mrf_ module
1. Clone the source code repository using the following command: `git clone https://github.com/lucianpls/mod_mrf.git`
1. In the `src/` directory, create a Makefile by copying from the provided example: `cp Makefile.lcl.example Makefile.lcl`
1. Edit **Makefile.lcl** modify the include paths (if needed) to reflect the **INCLUDES** include paths for apache2 on the server.  Also edit the `MOD_PATH` to match where apache2 modules are located on the filesystem.  This is a typical example:
```
INCLUDES = -I /usr/include/apache2 -I /usr/include/apr-1
MOD_PATH = /usr/lib64/apache2/
```
On some systems, the apache module path might be `/etc/httpd/modules` or `/usr/lib/apache2/modules`.  Note that the names **apache2** and **httpd** are sometimes used interchangeably.
1. Type `make` to build the module, and `make install` to install the resulting library file (for example, mod_mrf.so on linux) to the apache modules location.  Prefacing this with `sudo` may be required.
1. Add the module to Apache's module loader config file by editing the file `/etc/apache2/loadmodule.conf` and adding the following line at the end:
`LoadModule mrf_module      /usr/lib64/apache2-prefork/mod_mrf.so`
Note the `-prefork` in the path, and make sure that this path matches the apache2 install path on the system.  In other words, add `-prefork` to the end of the **MOD_PATH** from your Makefile, and then verify that the resulting path exists on the filesystem.  This is a directory created by Apache at runtime, so it may be necessary to restart on a system where Apache was newly installed.  At startup, Apache takes the modules from the **MOD_PATH** location and copies them to the prefork directory.
Note: On Ubuntu 16.04, no `-prefork` is created and the `so` file is placed in the same directory as specified
1. Add the mrf module to the list of **APACHE_MODULES** in the file `/etc/sysconfig/apache2`.  This is a space-delimited list of modules. Note that the module names do not have the **mod_** prefix or the **.so** suffix, so just add **mrf** to the end of this line.  (Note: This does not seem to exist on Ubuntu 16.04)
1. Restart Apache using the command: `sudo service apache2 restart`
1. Verify that the module is loaded by typing:
`sudo apachectl -M`
There should be a **mrf_module** line in the listing.  If not, troubleshoot the above steps.
Another way to list running modules is to use a browser to view the Apache server info page `http://localhost/server-info`.  Some Apache installs do not provide the server module required to view this page by default.  If the page does not load, it is probably because the info module isn't loaded in Apache.  To add this module, add the following line to `/etc/apache2/loadmodule.conf`:
`LoadModule mod_info_module      /usr/lib64/apache2-prefork/mod_info.so`
and also add **info** to the **APACHE_MODULES** line in `/etc/sysconfig/apache2`.  Finally, restart apache2 using the command in the previous step.

## Add the _mod_receivef_ module
1. Clone the source code repository using the following command: `git clone https://github.com/lucianpls/mod_receive.git`
1. Same as MRF example above.
1. Same as MRF example above.  The **HTTPD_INCLUDES_PATH** entry is just `/usr/include/apache2`, or whatever the main apache2 include path is in **INCLUDES**, depending on the system.
1. Same as MRF example above.
1. It does not appear to be necessary to add a LoadModule command to `/etc/apache2/loadmodule.conf` for this module.
1. Add **receive** to the list of **APACHE_MODULES** in the `/etc/sysconfig/apache2` file.
1. Restart Apache.
1. Verify that the **receive_module** is listed in the `apachectl -M` output.

## Add the _mod_sfim_ module
1. Clone the source code repository using the following command: `git clone https://github.com/lucianpls/mod_sfim.git`
1. Same as MRF example above.
1. Same as MRF example above, but only **MOD_PATH** variable path is required.
1. Same as MRF example above.
1. It does not appear to be necessary to add a LoadModule command to `/etc/apache2/loadmodule.conf` for this module.
1. Add **sfim** to the list of **APACHE_MODULES** in the `/etc/sysconfig/apache2` file.
1. Restart Apache.
1. Verify that the **sfim_module** is listed in the `apachectl -M` output.

## Add the _mod_reproject_ module
1. Clone the source code repository using the following command: `git clone https://github.com/lucianpls/mod_reproject.git` 
1. Same as MRF example above.
1. Same as MRF example above, but it may be necessary to add an additional `-I` include path to the mod_receivef source location, in order to access the `receive_context.h` file.
1. Same as MRF example above.  Building this module requires the development (includes headers) versions of the libraries **libapr-1** and **libjpeg**. Install these using the OS package manager if necessary.
1. It does not appear to be necessary to add a LoadModule command to `/etc/apache2/loadmodule.conf` for this module.
1. Add **reproject** to the list of **APACHE_MODULES** in the `/etc/sysconfig/apache2` file.
1. Restart Apache.
1. Verify that the **reproject_module** is listed in the `apachectl -M` output.

## Add the _mod_convert_ module
1. Clone the source code repository using the following command: `git clone https://github.com/lucianpls/mod_convert.git` 
1. Same as MRF example above.
1. Same as MRF example above, but it may be necessary to add an additional `-I` include path to the mod_receivef source location, in order to access the `receive_context.h` file.
1. Same as MRF example above.  Building this module requires the development (includes headers) versions of the libraries **libapr-1** and **libjpeg**. Install these using the OS package manager if necessary.
1. It does not appear to be necessary to add a LoadModule command to `/etc/apache2/loadmodule.conf` for this module.
1. Add **convert** to the list of **APACHE_MODULES** in the `/etc/sysconfig/apache2` file.
1. Restart Apache.
1. Verify that the **convert_module** is listed in the `apachectl -M` output.

At this point, the system is ready to operate as a WMS tile-serving engine.

## Configure Apache Virtual Host to Serve MRF Data
The Apache server has a directory from which web content is served.  This can be the default directory based on the install, or Apache can be configured with a Virtual Host that has special behavior based on the address of received requests.  AHTSE is configured to provide this behavior for the WMS data.

Configuring Apache with a Virtual Host is optional for AHTSE.  However, it provides flexibility with the web server so that it can be used for different types of content if so needed.  Some of the following steps would still be needed without a Virtual Host setup.

1. Add a configuration file in Apache's virtual hosts directory (e.g. `/etc/apache2/vhosts.d/`) by copying & renaming a template file provided in the install (e.g. **vhost.template**).
1. Modify the **\<VirtualHost\>** tag to match the hostname or URL that you want to be directed to AHTSE requests.
1. Set **\<DocumentRoot\>** to the Apache web content directory structure containing the **.wms** files.  See the wiki on importing MRF data sets, ".wms file" section for more information.
1. Add specific detail to **\<Directory\>** tag, including where **.wms** files are located in the Apache web content directory, server options, permissions.
1. Set log file locations for logging accesses and errors.

Here is an example from the Utah server configuration file `/etc/apache2/vhosts.d/openspace.conf`:
```
#(IP address below is fake)
<VirtualHost 000.000.000.000:80>
    ServerName openspace.sci.utah.edu
    DocumentRoot /srv/www/vhosts/openspace
    HostnameLookups Off
    UseCanonicalName Off
    ServerSignature Off
    <IfModule mod_userdir.c>
        UserDir public_html
        Include /etc/apache2/mod_userdir.conf
    </IfModule>
    <Directory "/srv/www/vhosts/openspace">
        Options Indexes FollowSymLinks
        AllowOverride None
        <IfModule !mod_access_compat.c>
            Require all granted
        </IfModule>
        <IfModule mod_access_compat.c>
            Order allow,deny
            Allow from all
        </IfModule>
    </Directory>
    ErrorLog /var/log/apache2/openspace/openspace_error_log
    LogLevel error
    TransferLog /var/log/apache2/openspace/openspace_access_log
</VirtualHost>
```
