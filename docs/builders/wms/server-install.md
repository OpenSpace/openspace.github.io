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

## Preparing building/compiling AHTSE modules/libraries

Create directories where modules were to be built.

```bash
mkdir ~/modules
mkdir ~/lib
mkdir ~/include
```

You will also add a line to the `/etc/ld.so.conf.d/libc.conf` where the `lib` is created.

Add the following line to the bottom of the file:

```conf
/home/[user]/lib
```

The libraries build will output to that directory, and will be used by Apache as a module.

## Building AHTSE modules/libraries

### Building `libicd` library

From the base directory (in this case `~/wms_modules`), `cd libicd/src/` and create a Makefile by copying from the provided example:

```bash
cp Makefile.lcl.example Makefile.lcl
```

Run `make` to build the dependencies, then `make install` to automatically place the dependencies in the correct location.

### Building `libahtse` module

From the base directory (in this case `~/wms_modules`), `cd libahtse/src/` and create a Makefile by copying from the provided example:

```bash
cp Makefile.lcl.example Makefile.lcl
```

Run `make` to build the dependencies, then `make install` to automatically place the dependencies in the correct location.

### Building `mod_mrf` module

From the base directory (in this case `~/wms_modules`), `cd mod_mrf/src/` and create a Makefile by copying from the provided example:

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

### Building `mod_convert`

From the base directory (in this case `~/wms_modules`), `cd mod_convert/src/` and create a Makefile by copying from the provided example:

```bash
cp Makefile.lcl.example Makefile.lcl
```

Run `make` to build the dependencies, then `make install` to automatically place the dependencies in the correct location.

### Building `mod_receive`

From the base directory (in this case `~/wms_modules`), `cd mod_receive/src/` and create a Makefile by copying from the provided example:

```bash
cp Makefile.lcl.example Makefile.lcl
```

Run `make` to build the dependencies, then `make install` to automatically place the dependencies in the correct location.

### Building `mod_reproject`

From the base directory (in this case `~/wms_modules`), `cd mod_reproject/src/` and create a Makefile by copying from the provided example:

```bash
cp Makefile.lcl.example Makefile.lcl
```

Run `make` to build the dependencies, then `make install` to automatically place the dependencies in the correct location.

**Note: The module generated is `mod_retile`, this is still the same module, just renamed.**

### Building `mod_sfim`

From the base directory (in this case `~/wms_modules`), `cd mod_sfim/src/` and create a Makefile by copying from the provided example:

```bash
cp Makefile.lcl.example Makefile.lcl
```

Run `make` to build the dependencies, then `make install` to automatically place the dependencies in the correct location.

## Installing modules for Apache

### Installing `mod_mrf`

To install `mod_mrf`, you need to create a new Apache module in `/etc/apache2/mods-available` called `mrf.load`.

The contents of this file will consist of:

```conf
LoadFile /home/[user]/modules/libahtse.so
LoadModule mrf_module /home/[user]/modules/mod_mrf.so
```

Create a soft-symlink to `mods-enabled` via this command:

```bash
ln -s /etc/apache2/mods-available/mrf.load /etc/apache2/mods-enabled/mrf.load
```

You may need `sudo` to execute.

Restart the Apache server with `sudo apachectl restart`, there will be a message that looks like:

To verify if the module is loaded, run `sudo apachectl -M` and check if `mrf_module` is loaded.

### Installing `mod_convert`

To install `mod_convert`, you need to create a new Apache module in `/etc/apache2/mods-available` called `convert.load`.

The contents of this file will consist of:

```conf
LoadModule convert_module /home/[user]/modules/mod_convert.so
```

Create a soft-symlink to `mods-enabled` via this command:

```bash
ln -s /etc/apache2/mods-available/convert.load /etc/apache2/mods-enabled/convert.load
```

You may need `sudo` to execute.

Restart the Apache server with `sudo apachectl restart`, there will be a message that looks like:

To verify if the module is loaded, run `sudo apachectl -M` and check if `convert_module` is loaded.

### Installing `mod_receive`

To install `mod_receive`, you need to create a new Apache module in `/etc/apache2/mods-available` called `receive.load`.

The contents of this file will consist of:

```conf
LoadModule receive_module /home/[user]/modules/mod_receive.so
```

Create a soft-symlink to `mods-enabled` via this command:

```bash
ln -s /etc/apache2/mods-available/receive.load /etc/apache2/mods-enabled/receive.load
```

You may need `sudo` to execute.

Restart the Apache server with `sudo apachectl restart`, there will be a message that looks like:

To verify if the module is loaded, run `sudo apachectl -M` and check if `receive_module` is loaded.

### Installing `mod_retile`

To install `mod_retile`, you need to create a new Apache module in `/etc/apache2/mods-available` called `retile.load`.

The contents of this file will consist of:

```conf
LoadModule retile_module /home/[user]/modules/mod_retile.so
```

Create a soft-symlink to `mods-enabled` via this command:

```bash
ln -s /etc/apache2/mods-available/retile.load /etc/apache2/mods-enabled/retile.load
```

You may need `sudo` to execute.

Restart the Apache server with `sudo apachectl restart`, there will be a message that looks like:

To verify if the module is loaded, run `sudo apachectl -M` and check if `retile_module` is loaded.

### Installing `mod_sfim`

To install `mod_sfim`, you need to create a new Apache module in `/etc/apache2/mods-available` called `sfim.load`.

The contents of this file will consist of:

```conf
LoadModule sfim_module /home/[user]/modules/mod_sfim.so
```

Create a soft-symlink to `mods-enabled` via this command:

```bash
ln -s /etc/apache2/mods-available/sfim.load /etc/apache2/mods-enabled/sfim.load
```

You may need `sudo` to execute.

Restart the Apache server with `sudo apachectl restart`, there will be a message that looks like:

To verify if the module is loaded, run `sudo apachectl -M` and check if `sfim_module` is loaded.

## Configure Apache Virtual Host to Serve MRF Data

The Apache server has a directory from which web content is served. This can be the default directory based on the install, or Apache can be configured with a Virtual Host that has special behavior based on the address of received requests.

AHTSE is configured to provide this behavior for the WMS data.

Configuring Apache with a Virtual Host is optional for AHTSE. However, it provides flexibility with the web server so that it can be used for different types of content if so needed.

Some of the following steps would still be needed without a Virtual Host setup.

1. Add a configuration file in Apache's virtual hosts directory (e.g. `/etc/apache2/vhosts.d/`) by copying & renaming a template file provided in the install (e.g. **vhost.template**).
2. Modify the **\<VirtualHost\>** tag to match the hostname or URL that you want to be directed to AHTSE requests.
3. Set **\<DocumentRoot\>** to the Apache web content directory structure containing the **.wms** files.  See the wiki on importing MRF data sets, ".wms file" section for more information.
4. Add specific detail to **\<Directory\>** tag, including where **.wms** files are located in the Apache web content directory, server options, permissions.
5. Set log file locations for logging accesses and errors.

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
