---
title: Server Install
layout: default

grand_parent: Builders
parent: WMS
nav_order: 1
---

This wiki covers the steps required to get an OpenSpace WMS (Web Map Server) configured & running. This serves MRF (Meta Raster Format) files. Another name for this service is AHTSE (An Httpd/Apache Tile-Serving Engine).
[This wiki](server-import) covers the steps involved in importing WMS dataset(s) so that the AHTSE can serve tiles from the set. [This wiki](server-conversion) covers the steps involved in converting a raw raster image into the MRF format.

These instructions are specific to a Ubuntu Linux 22.04 server install. However other Linux distributions can work with some packages or paths changed around.

## Web Server Setup

Install the following software for getting AHTSE up and running:

- Apache web server (`apache2`)
- Apache web server developer headers (`apache2-dev`)
- Geospatial Data Abstraction Library (GDAL) (`gdal-bin`)
- GDAL developer package (`libgdal-dev`)
- Git (`git`)
- Make (`build-essential`)
- GNU C/C++ compilers (`g++`/`gcc`)

For example on downloading this via Ubuntu 22.04 LTS:

```bash
sudo apt install apache2 apache2-dev gdal-bin libgdal-dev build-essential gcc g++
```

## Obtaining AHSTE dependencies

Some, but not all, modules require include files from other modules or related libraries. So all necessary repositories will be cloned first before building any of them.

1. Create a base directory in which all modules will be cloned (e.g. `mkdir ~/wms_modules`).
2. `cd` into the directory created from last step
3. Clone each of these repositories from the base directory (a subdirectory will automatically be created in the base directory for each repository):

- `git clone https://github.com/lucianpls/libahtse.git`
- `git clone https://github.com/lucianpls/AHTSE.git`
- `git clone https://github.com/lucianpls/libicd.git`
- `git clone https://github.com/lucianpls/mod_mrf.git`
- `git clone https://github.com/lucianpls/mod_receive.git`
- `git clone https://github.com/lucianpls/mod_sfim.git`
- `git clone https://github.com/lucianpls/mod_reproject.git`
- `git clone https://github.com/lucianpls/mod_convert.git`

Ensure all the directories are next to each other, this is important for building the modules as they reference each other.

## Preparing building/compiling AHTSE modules

Create directories where modules were to be built.

```bash
mkdir ~/modules
mkdir ~/lib
mkdir ~/include
```

## Building `mod_mrf` module

From the base directory, `cd mod_mrf/src/` and create a Makefile by copying from the provided example:

```bash
cp Makefile.lcl.example Makefile.lcl
```

Edit `Makefile.lcl`, find the line that defines `EXTRA_INCLUDES`, and add the following lines _below_ that line:

```makefile
EXTRA_INCLUDES += -I../../libahtse/src
EXTRA_INCLUDES += -I../../libicd/src
EXTRA_INCLUDES += -I../../mod_receive/src
```

Type `make` to build the module, and `make install` to install the resulting library file in `~/modules` to the apache modules location.

Add the module to Apache's `modules-available` by creating the file `/etc/apache2/modules-available/mrf.load` and adding the line:

```conf
LoadModule mrf_module /usr/lib64/apache2-prefork/mod_mrf.so
```

Note the `-prefork` in the path, and make sure that this path matches the apache2 install path on the system.  In other words, add `-prefork` to the end of the **MOD_PATH** from your Makefile, and then verify that the resulting path exists on the filesystem.  This is a directory created by Apache at runtime, so it may be necessary to restart on a system where Apache was newly installed.  At startup, Apache takes the modules from the **MOD_PATH** location and copies them to the prefork directory.

Restart Apache using the command: `sudo apachectl restart`

Verify that the module is loaded by typing: `sudo apachectl -M`

There should be a **mrf_module** line in the listing.  If not, troubleshoot the above steps.

Another way to list running modules is to use a browser to view the Apache server info page `http://localhost/server-info`.  Some Apache installs do not provide the server module required to view this page by default.  If the page does not load, it is probably because the info module isn't loaded in Apache.  To add this module, add the following line to `/etc/apache2/loadmodule.conf`:

`LoadModule mod_info_module /usr/lib64/apache2-prefork/mod_info.so`
and also add **info** to the **APACHE_MODULES** line in `/etc/sysconfig/apache2`.  Finally, restart apache2 using the command in the previous step.

## Add the `mod_receivef`module

1. From the base directory, `cd mod_receive/src/` and create a Makefile by copying from the provided example: `cp Makefile.lcl.example Makefile.lcl`
2. No **EXTRA_INCLUDES** definitions are needed for this module.
3. Same as MRF example above.
4. It does not appear to be necessary to add a LoadModule command to `/etc/apache2/loadmodule.conf` for this module.
5. Add **receive** to the list of **APACHE_MODULES** in the `/etc/sysconfig/apache2` file.
6. Restart Apache.
7. Verify that the **receive_module** is listed in the `apachectl -M` output.

## Add the `mod_sfim` module

1. From the base directory, `cd mod_sfim/src/` and create a Makefile by copying from the provided example: `cp Makefile.lcl.example Makefile.lcl`
2. No **EXTRA_INCLUDES** definitions are needed for this module.
3. Same as MRF example above.
4. It does not appear to be necessary to add a LoadModule command to `/etc/apache2/loadmodule.conf` for this module.
5. Add **sfim** to the list of **APACHE_MODULES** in the `/etc/sysconfig/apache2` file.
6. Restart Apache.
7. Verify that the **sfim_module** is listed in the `apachectl -M` output.

## Add the `mod_reproject` module

1. From the base directory, `cd mod_reproject/src/` and create a Makefile by copying from the provided example: `cp Makefile.lcl.example Makefile.lcl` 
2. Add the 3 additional **EXTRA_INCLUDES** lines to Makefile.lcl, as described in the mrf module instructions above.
3. Same as MRF example above.
4. It does not appear to be necessary to add a LoadModule command to `/etc/apache2/loadmodule.conf` for this module.
5. Add **reproject** to the list of **APACHE_MODULES** in the `/etc/sysconfig/apache2` file.
6. Restart Apache.
7. Verify that the **reproject_module** is listed in the `apachectl -M` output.

## Add the `mod_convert` module

1. From the base directory, `cd mod_convert/src/` and create a Makefile by copying from the provided example: `cp Makefile.lcl.example Makefile.lcl`
2. Add the 3 additional **EXTRA_INCLUDES** lines to Makefile.lcl, as described in the mrf module instructions above.
3. Same as MRF example above.
4. It does not appear to be necessary to add a LoadModule command to `/etc/apache2/loadmodule.conf` for this module.
5. Add **convert** to the list of **APACHE_MODULES** in the `/etc/sysconfig/apache2` file.
6. Restart Apache.
7. Verify that the **convert_module** is listed in the `apachectl -M` output.

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

```apache
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
