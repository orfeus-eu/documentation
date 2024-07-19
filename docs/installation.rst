EIDA System configuration (using SeisComP3 - partially outdated) 
===============================================================

Written by Jan Michalek (2019) 

.. General procedure

| `SEISCOMP3 installation`_
| `Example installation of compiled version`_
| `Compiling SEISCOMP3 (example)`_
| `SEISCOMP3 configuration`_
| `Enable modules`_
| `Networks and Stations configuration`_
| `Bindings configuration`_
| `SEEDLINK profile`_
| `GLOBAL profile`_
| `SCAUTOPICK profile`_
| `Monitoring windows`_
| `Location configuration`_
| `Extracts from SC3`_
| `SCRTTV`_
| `SCMV`_
| `SCQC`_
| `Configure FDSN web services in your SC3`_
| `Excluding stations from FDSNWS`_

.. General procedure
.. -----------------

.. Install SeisComP3 (SC3)
.. Configure SC3
.. Enable modules
.. Import station metadata
.. Create bindings
.. SEEDLINK
.. ARCLINK
.. SLARCHIVE
.. Configure SC3 modules
.. FDSNWS module
.. ARCLINK module
.. SLARCHIVE module
.. GLOBAL module
.. Install and configure WebDC3 web interface
.. Install EIDA tools
.. WFCatalog
.. Enable WFCatalog GUI web interface
.. Routing service

.. SEISCOMP3

It might be convenient to create a ``sysop`` user on the server where SC3 will be installed. Most of the manuals are describing installation into ``/home/sysop/`` folder.

SEISCOMP3 installation
----------------------

There are 2 options how to get SC3:

* Make clone from GitHub repository (requires compilation from source code; https://github.com/SeisComP3/seiscomp3;). There are instructions for cloning and compilation in README file.

* Download compiled version according to your OS Follow installation instructions (https://www.seiscomp3.org/downloader/).

**License**

Institution needs to have license files to be able to run programs in SC3. To obtain license follow instructions here: https://www.seiscomp3.org/license.html


Example installation of compiled version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For Ubuntu 14.04 32-bit:

| Download: seiscomp3-seattle-2014.084.01-ubuntu14.04-i686.tar.gz
| Download: seiscomp3-seattle-2014.084.01-doc.tar.gz
| Download: seiscomp3-seattle-maps.tar.gz

In your home directory (in the example ``/home/sysop``): ::

    $ tar -xvfz seiscomp3-seattle-2014.084.01-ubuntu14.04-i686.tar.gz
    $ tar -xvfz seiscomp3-seattle-2014.084.01-doc.tar.gz
    $ tar -xvfz seiscomp3-seattle-maps.tar.gz

Your license key files must be installed in ``/home/sysyop/.seiscomp3/key/``

| Files: (``License``,  ``License.key``, ``License.signed``)

Add to your ``.bashrc`` file: ::

    # SEISCOMP3
    export SEISCOMP_ROOT=/home/sysop/seiscomp3
    export PATH=/home/sysop/seiscomp3/bin:$PATH
    export LD_LIBRARY_PATH=/home/sysop/seiscomp3/lib:$LD_LIBRARY_PATH
    export PYTHONPATH=/home/sysop/seiscomp3/lib/python:$PYTHONPATH
    export MANPATH=/home/sysop/seiscomp3/share/man:$MANPATH
    export LC_ALL=C

Open SEISCOMP3 online documentation, click Installation, and install what is listed under Install dependencies. Names of the packages can be slightly different.

Compiling SEISCOMP3 (example)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Follow instructions on GitHub: https://github.com/SeisComP3/seiscomp3/tree/c3597388ba0af8635a6818783cafcf493d0f0cce

Be sure to have all dependencies solved beforehand. For Ubuntu 16.04: ::

    $ sudo apt-get install libqt4-dev pkg-config python-m2crypto libncurses5-dev libncursesw5-dev libxml2-dev libboost-all-dev mysql-client libmysqlclient-dev


Copy source code: ::

    $ git clone https://github.com/SeisComP3/seiscomp3.git sc3-src
    $ cd sc3-src

Change to latest release, e.g.: ::

    $ git checkout release/jakarta/2017.334.05

Configure and prepare the build: ::

    $ make -f Makefile.cvs
    $ # Press “c”, “c” and “g”
    $ cd build
    $ # This step can take ~25 minutes
    $ make
    $ make install


If you haven’t changed path via ``-DCMAKE_INSTALL_PREFIX=/path/to/install/dir`` parameter then the compiled version is copied directly to ``~/seiscomp3/``.


SEISCOMP3 configuration
~~~~~~~~~~~~~~~~~~~~~~~

Next step is to configure SC3. Be sure you have your MySQL root password, then run following: ::

    $ seiscomp setup


Fill in the values appropriately, or keep default values. ::

    Agency ID []:
    Datacenter ID []:
    Organization string []:
    Enable database storage [yes]:
    0) mysql

    * MySQL server.

    1) postgresql

    *  Postgresql server. There is currently no support in setup to create the database for you. You have to setup the database and user accounts on your own. The database schema is installed under share/db/postgresql.sql.  Note that the database encoding should be UTF8 and that you need to set the encoding to 'escape' for PostgreSQL >= 9, e.g. "ALTER DATABASE seiscomp3 SET bytea_output TO 'escape';"

    Database backend [0]:
    Create database [yes]:
    MYSQL root password (input not echoed) []:
    Drop existing database [no]:
    Database name [seiscomp3]:
    Database hostname [localhost]:
    Database read-write user [sysop]:
    Database read-write password [sysop]:
    Database public hostname [localhost]:
    Database read-only user [sysop]:
    Database read-only password [sysop]:

Finish setup
~~~~~~~~~~~~

Finally, ::

    P) Proceed to apply configuration
    B) Back to last parameter
    Q) Quit without changes
    Command? [P]:
    Running setup
    * setup kernel
    * setup scmaster
    + Create MYSQL database
     + Found MYSQL server version 5.5.37-0ubuntu0.14.04.1
     + Drop database seiscomp3
     + Create database seiscomp3
     + Setup user roles
     + Create tables
    * setup trunk
    sysop@home:~$

Enable modules
~~~~~~~~~~~~~~

From command line enabled seedlink: ::

    $ seiscomp enable seedlink [scautopick scautoloc scamp scmag scevent]
    $ seiscomp start

Start the graphical configuration tool: ::

    $ seiscomp exec scconfig

or ::

    $ scconfig


Networks and Stations configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Start ``scconfig``
* Go to "Inventory" and press "Import"
* Select "dslv" and browse to find your SEED station response file(s)
* Press "Test sync"
* Press "Sync"
* Press "Sync keys"
* Save config


Bindings configuration
~~~~~~~~~~~~~~~~~~~~~~

| enter Bindings
| Your network should be visible under Networks and in the window below

SEEDLINK profile
~~~~~~~~~~~~~~~~

* right click on seedlink (right-upper corner of the window) and type profile name (SLINK). If you are receiving data directly from station then it is wise to use name of the station for the profile. If you are receiving data from another server (multiple stations) then use name of the server. Each seedlink connection needs to have its own binding profile.

* double-click on the SLINK profile

| go down to sources
| click on the '+'
| give a name to the seedlink source (STA-SEEDLINK)
| now under sources :
| expand STA-SEEDLINK: chain
| [open selectors and type :  HH?.D]
| check that address and port is correct
| do save

GLOBAL profile
~~~~~~~~~~~~~~

GLOBAL profile is needed for some other modules to be working (scrttv, scmv, ...)

| add global profile: GLOBAL
| double-click on GLOBAL
| enter HHZ on detectStream
| do save

SCAUTOPICK profile
~~~~~~~~~~~~~~~~~~

| add scautopick profile SCAUTOPICK
| double click on SCAUTOPICK
| change filter to 2.0-8.0
| do save

| Drag profiles SLINK [+ GLOBAL + SCAUTOPIC] to network on the left

| enter System
| Update configuration

Monitoring windows
~~~~~~~~~~~~~~~~~~

Now open new terminal and run e.g. scrttv, scmv or scolv


Location configuration
~~~~~~~~~~~~~~~~~~~~~~

* check /home/sysop/seiscomp3/etc/defaults/scevent.cfg for parameters to locate an event
* check doc: file:///home/sysop/seiscomp3/share/doc/seiscomp3/html/apps/stationconf.html for adding stations
* manual configuration can be entered via ::

    $ seiscomp exec stationconf
    $ seiscomp update-config

Extracts from SC3
~~~~~~~~~~~~~~~~~

ALL NETWORKS,ALL CHANNELS,ALL COMPONENTS ::

    $ scart -dsvE -t '2015-07-18 00:00~2015-07-18 23:00' ~/seiscomp3/var/lib/archive > sorted.mseed


NETWORKS,CHANNELS AND COMPONENTS specified in list.txt ::

    $ scart -dsvE -l list.txt ~/seiscomp3/var/lib/archive > sorted.mseed

    $ cat list.txt
    2015-07-20 07:50;2015-07-20 07:58;CX.PB02.*.*
    2015-07-20 07:50;2015-07-20 07:58;CX.PB01.*.*
    2015-07-20 07:50;2015-07-20 07:58;CX.PB04..BHZ



Extract n minutes from eventid: gfz2015nzbb and create mseed file redable from SEISAN ::

    scevtstreams -E gfz2015nzbb -d mysql://sysop:sysop@localhost/seiscomp3 -L 0 -m 300 | scart -dsvE --list - ~/seiscomp3/var/lib/archive > gfz2015nzbb-sorted.mseed



Extract inventory from database ( must be interpreted to find lat, lon, height, response etc ::

    scxmldump -I -d  mysql://sysop:sysop@localhost/seiscomp3 -o inventory.xml

SCRTTV
------

To enable streams in scrttv:

* In scconfig GUI go to Modules -> GUI -> scrttv
* modify streams -> codes
* change from “default” to * (wild card for all)

SCMV
----

| Problem: Stations displayed but as black, i.e. no amplitude values.

| Solution: Edit global binding profile.

| detecStream: HHZ (I tried "HH" and "HH*" before but it didn't work)

| detecLocid: 00

| Ctrl+S, Update configuration

SCQC
----

| Module scqc must be enabled and global binding profile applied to networks. It uses the same profile configuration as by SCMV.

| EDIT: Configuration of scqc module can be modified to be independent on global binding profile:

| Uncheck scqc.useConfiguredStreams

**ISSUE: conflict SCMV configuration with SCRTTV**

| Global binding profile is required by SCMV module (to see stations in colors in GUI). However setting up this profile restricts streams in SCRTTV to those streams in global binding profile (attributes: detecStream, detecLocid). Using multiple streams in global binding profile does not work (e.g. BHZ, HHZ; or ?HZ).

| Partial solution for SCRTTV: Modules -> GUI -> scrttv -> streams: *.*.*.?H?    

| Then channels become visible.

Configure FDSN web services in your SC3
---------------------------------------

Open ``scconfig`` ::

    $ scconfig

Click on the “Modules” icon and go to the “global” module.\
Look for the “database” section and complete the following: ::

    type=mysql
    parameters=sysop:sysop@localhost/seiscomp3

Press Ctrl+S to save the configuration.\
Go to the “fdsnws” module in the tree on the left. Then, go to the “global” section and the “recordstream” subsection and complete with the following: ::

    service=sdsarchive
    source=/home/sysop/seiscomp3/var/lib/archive

Press Ctrl+S to save the configuration.\
Click to the “System” icon, click on “Update configuration” and restart SeisComP3

Excluding stations from FDSNWS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| done via filter file; e.g.: ``/home/sysop/seiscomp3/etc/fdsnws_filter.ini``
| description: https://www.seiscomp3.org/doc/jakarta/current/apps/fdsnws.html#filtering-the-inventory
| Add path to your filter file to Modules -> fdsnws -> “stationFilter” and “dataSelectFilter”
| use full-path; ``$SEISCOMP_ROOT/etc/fdsnws_filter.ini`` does not work

| Exclude rules must be defined BEFORE include rules, otherwise exclude rules are not applied

| Content of FDSNWS inventory can be checked as follows:
| in scconfig go to Modules -> fdsnws -> check the “debugFilter” ON (Ctrl+S; Update configuration)
| turn off fdsnws in System

From command line run: ::

    fdsnws --debug

As this starts it writes down all streams and whether they are included or not
| Stop fdsnws in command line (Ctrl+C)
| Disable the “debugFilter” (Ctrl+S; Update configuration)
| Restart FDSNWS module in System

Make test query to FDSN: ::

    curl -X GET "localhost:8080/fdsnws/station/1/query?sta=*"

