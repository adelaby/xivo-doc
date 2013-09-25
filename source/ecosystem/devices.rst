.. _devices:

*******
Devices
*******

Supported device (Official support)
===================================

XiVO provides official support for the following phones. These phones will be supported across upgrades and phone features are guaranteed to be supported on the latest version.

Aastra
------

6700i series:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
6731i    |y|         8          |y|
6735i    |y|         26         |y|
6737i    |y|         30         |y|
6739i    |y|         55         |y|
6755i    |y|         26         |y|
6757i    |y|         30         |y|
======== =========== ========== ============

The M670i and M675i expansion modules are supported.

DECT Infrastructure:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
RFP35    |n| [4]_    0          |n|
RFP36    |n| [4]_    0          |n|
======== =========== ========== ============


Cisco
-----

ATAs:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
SPA122   |n| [4]_    0          |n|
SPA3102  |n| [4]_    0          |n|
SPA8000  |y|         0          |n|
======== =========== ========== ============

.. note::
   For best results, activate :ref:`dhcp-integration` on your XiVO.

.. note::
   These devices can be used to connect Faxes. For better success with faxes some parameters
   must be changed. You can read the :ref:`fax-analog-gateway` section.

.. note::
   If you want to manually resynchronize the configuration from the ATA device 
   you should use the following url::

     http://ATA_IP/admin/resync?http://XIVO_IP:8667/CONF_FILE

   where :

      * *ATA_IP*    is the IP address of the ATA,
      * *XIVO_IP*   is the IP address of your XiVO,
      * *CONF_FILE* is one of ``spa3102.cfg``, ``spa8000.cfg``

.. warning:: SCCP phones are supported, but limited to the features supported in XIVO's SCCP implementation.

Cisco 7900 series (*SCCP* mode only):

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
7905G    |n| [4]_    0          |n|
7906G    |y|         0          |y|
7911G    |y|         0          |y|
7912G    |y|         0          |y|
7920     |y|         0          |y|
7921G    |y|         0          |y|
7940G    |y|         0          |y|
7941G    |y|         0          |y|
7941G-GE |y|         0          |y|
7942G    |y|         0          |y|
7960G    |y|         0          |y|
7961G    |y|         0          |y|
7962G    |y|         0          |y|
======== =========== ========== ============

.. _cisco-provisioning:

To install firmware for xivo-cisco-sccp plugins, you need to manually download
the firmware files from the Cisco website and save them in the
:file:`/var/lib/xivo-provd/plugins/$plugin-name/var/cache` directory.

.. note::
   The directory is created by XiVO when you install the plugin (i.e. xivo-cisco-sccp-legacy).
   If you create the directory manually, the installation may fail!

For example, if you have installed the ``xivo-cisco-sccp-legacy`` plugin and you want to install the ``7940-7960-fw``, ``networklocale`` and ``userlocale_fr_FR`` package, you must:

* Go to http://www.cisco.com
* Click on "Log In" in the top right corner of the page, and then log in
* Click on the "Support" menu
* Click on the "Downloads" tab, then on "Voice & Unified Communications"
* Select "IP Telephony", then "Unified Communications Endpoints", then the model of your phone (in this example, the 7940G)
* Click on "Skinny Client Control Protocol (SCCP) software"
* Choose the same version as the one shown in the plugin
* Download the file with an extension ending in ".zip", which is usually the last file in the list
* In the XiVO web interface, you'll then be able to click on the "install" button for the firmware

The procedure is similar for the network locale and the user locale package, but:

* Instead of clicking on "Skinny Client Control Protocol (SCCP) software", click on "Unified Communications Manager Endpoints Locale Installer"
* Click on "Linux"
* Choose the same version of the one shown in the plugin
* For the network locale, download the file named "po-locale-combined-network.cop.sgn"
* For the user locale, download the file named "po-locale-$locale-name.cop.sgn, for example "po-locale-fr_FR.cop.sgn" for the "fr_FR" locale
* Both files must be placed in :file:`/var/lib/xivo-provd/plugins/$plugin-name/var/cache` directory. Then install them in the XiVO Web Interface.

.. note:: Currently user and network locale 9.0.2 should be used for plugins xivo-sccp-legacy and xivo-cisco-sccp-9.0.3


Digium
------

Digium phones:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
D40      |y|         2          |n|
D50      |n| [4]_    14         |n|
D70      |y|         106        |n|
======== =========== ========== ============

.. note:: Some function keys are shared with line keys

Particularities:

* For best results, activate :ref:`dhcp-integration` on your XiVO.
* English is the only language supported, other languages (e.g. french) are not supported.
* Impossible to do directed pickup using a BLF function key.
* Only supports DTMF in RFC2833 mode.
* Does not work reliably with Cisco ESW520 PoE switch. When connected to such a switch, the D40 tends to reboot randomly, and the D70 does not boot at all.
* It's important to not edit the phone configuration via the phones' web interface when using these phones with XiVO.
* Paging doesn't work.


Polycom
-------

SoundPoint IP:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
SPIP331  |n| [4]_    0          |n|
SPIP335  |y|         0          |n|
SPIP450  |y|         2          |n|
SPIP550  |y|         3          |n|
SPIP560  |n| [4]_    3          |n|
SPIP650  |n| [4]_    47         |n|
======== =========== ========== ============

SoundStation IP:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
SPIP5000 |n| [4]_    0          |n|
SPIP6000 |y|         0          |n|
SPIP7000 |n| [4]_    0          |n|
======== =========== ========== ============

Others:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
VVX300   |n| [4]_    6          |n|
VVX400   |n| [4]_    12         |n|
VVX500   |n| [4]_    |u|        |n|
VVX600   |n| [4]_    |u|        |n|
======== =========== ========== ============

Polycom® SoundPoint® IP Backlit Expansion Module are supported.


Snom
----

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
370      |n| [4]_    12         |y|
710      |y|         5          |y|
720      |y|         18         |y|
760      |y|         12         |y|
821      |ny|        |u|        |u|
870      |y|         15         |y|
======== =========== ========== ============

Snom Vision – the expansion module for snom 8xx series VoIP telephones are supported.

Snom extension modules V2.0 are supported.

.. note:: For some models, function keys are shared with line keys

.. warning:: If you are using Snom phones with HA, you should not assign multiple lines to the same device.

There's a known issue with the provisioning of Snom phones in XiVO:

* After a factory reset of a phone, if no language and timezone are set for the "default config device" in :menuselection:`XiVO --> Configuration --> Provisioning --> Template device`, you will be forced to select a default language and timezone on the phone UI.


Yealink
-------

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
T18P     |n| [4]_    |u|        |n|
T22P     |n| [4]_    3          |n|
T28P     |y|         16         |n|
T32G     |n| [4]_    3          |n|
T38G     |y|         16         |n|
T42G     |n| [4]_    |u|        |n|
T46G     |ny|        |u|        |u|
W52P     |y|         |u|        |n|
======== =========== ========== ============

.. note:: Some function keys are shared with line keys

The EXP38 and EXP39 expansion modules are supported.


Compatible device (Community support)
=====================================

The following phones are only supported by the community. In other words, maintenance, bug corrections and features are developed by members of the XiVO community. XiVO does not officially endorse support for these phones.


Aastra
------

6700i and 9000i series:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
6730i    |n|         8          |y|
6751i    |n|         |u|        |y|
6753i    |y|         6          |y|
6757i    |y|         30         |y|
9143i    |y|         7          |y|
9480i    |n|         6          |y|
9480CT   |n|         6          |y|
======== =========== ========== ============


Alcatel-Lucent
--------------

IP Touch series:

====================== =========== ========== ============
Model                  Tested [1]_ Fkeys [2]_ XiVO HA [3]_
====================== =========== ========== ============
4008 Extended Edition  |y|         4          |n|
4018 Extended Edition  |y|         4          |n|
====================== =========== ========== ============

Note that you *must not* download the firmware for these phones unless you
agree to the fact it comes from a non-official source.

For the plugin to work fully, you need these additional packages::

   apt-get install p7zip python-pexpect telnet


Avaya
-----

1200 series IP Deskphones (previously known as Nortel IP Phones):

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
1220 IP  |y|         0          |n|
1230 IP  |n|         0          |n|
======== =========== ========== ============


Cisco
-----

Cisco Small Business SPA300 series:

=========== =========== ========== ============
Model       Tested [1]_ Fkeys [2]_ XiVO HA [3]_
=========== =========== ========== ============
SPA301      |n|         1          |n|
SPA303      |n|         3          |n|
=========== =========== ========== ============

.. note:: Function keys are shared with line keys for all SPA phones

Cisco Small Business SPA500 series:

=========== =========== ========== ============
Model       Tested [1]_ Fkeys [2]_ XiVO HA [3]_
=========== =========== ========== ============
SPA501G     |y|         8          |n|
SPA502G     |n|         1          |n|
SPA504G     |y|         4          |n|
SPA508G     |y|         8          |n|
SPA509G     |n|         12         |n|
SPA525G     |y|         5          |n|
SPA525G2    |n|         5          |n|
=========== =========== ========== ============

The SPA500 expansion module is supported.

Cisco Small Business IP Phones (previously known as Linksys IP Phones)

=========== =========== ========== ============
Model       Tested [1]_ Fkeys [2]_ XiVO HA [3]_
=========== =========== ========== ============
SPA901      |n|         1          |n|
SPA921      |n|         1          |n|
SPA922      |n|         1          |n|
SPA941      |n|         4          |n|
SPA942      |y|         4          |n|
SPA962      |y|         6          |n|
=========== =========== ========== ============

.. note:: You must install the firmware of each SPA9xx phones you are using since they reboot in
          loop when they can’t find their firmware.

The SPA932 expansion module is supported.

ATAs:

=========== =========== ========== ============
Model       Tested [1]_ Fkeys [2]_ XiVO HA [3]_
=========== =========== ========== ============
PAP2        |n|         0          |n|
SPA2102     |n|         0          |n|
SPA8800     |n|         0          |n|
=========== =========== ========== ============

   For best results, activate :ref:`dhcp-integration` on your XiVO.

.. note::
   These devices can be used to connect Faxes. For better success with faxes some parameters
   must be changed. You can read the :ref:`fax-analog-gateway` section.

.. note::
   If you want to manually resynchronize the configuration from the ATA device 
   you should use the following url::

     http://ATA_IP/admin/resync?http://XIVO_IP:8667/CONF_FILE

   where :

      * *ATA_IP*    is the IP address of the ATA,
      * *XIVO_IP*   is the IP address of your XiVO,
      * *CONF_FILE* is one of ``spa2102.cfg``, ``spa8000.cfg``


Gigaset
-------

Also known as Siemens.

=========== =========== ========== ============
Model       Tested [1]_ Fkeys [2]_ XiVO HA [3]_
=========== =========== ========== ============
C470 IP     |n|         0          |n|
C475 IP     |n|         0          |n|
C590 IP     |n|         0          |n|
C595 IP     |n|         0          |n|
C610 IP     |n|         0          |n|
C610A IP    |n|         0          |n|
S675 IP     |n|         0          |n|
S685 IP     |n|         0          |n|
N300 IP     |n|         0          |n|
N300A IP    |n|         0          |n|
N510 IP PRO |n|         0          |n|
=========== =========== ========== ============


Jitsi
-----

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
Jitsi    |y|         |u|        |n|
======== =========== ========== ============


Panasonic
---------

Panasonic KX-HTXXX series:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
KX-HT113   |n|         |u|         |n|
KX-HT123   |n|         |u|         |n|
KX-HT133   |n|         |u|         |n|
KX-HT136   |n|         |u|         |n|
======== =========== ========== ============

.. note:: This phone is for testing for the moment


Polycom
-------

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
SPIP320  |n|         0          |n|
SPIP321  |n|         0          |n|
SPIP330  |n|         0          |n|
SPIP430  |n|         0          |n|
SPIP501  |y|         0          |n|
SPIP600  |n|         0          |n|
SPIP601  |n|         0          |n|
SPIP670  |n|         47         |n|
======== =========== ========== ============

SoundStation IP:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
SPIP4000 |n|         0          |n|
======== =========== ========== ============

Others:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
VVX1500  |n|         0          |n|
======== =========== ========== ============


Snom
----

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
300      |n|         6          |y|
320      |y|         12         |y|
360      |n|         |u|        |y|
820      |y|         4          |y|
MP       |n|         |u|        |y|
PA1      |n|         0          |y|
======== =========== ========== ============

.. note:: For some models, function keys are shared with line keys

.. warning:: If you are using Snom phones with HA, you should not assign multiple lines to the same device.

There's a known issue with the provisioning of Snom phones in XiVO:

* After a factory reset of a phone, if no language and timezone are set for the "default config device" in :menuselection:`XiVO --> Configuration --> Provisioning --> Template device`, you will be forced to select a default language and timezone on the phone UI.


Technicolor
-----------

Previously known as Thomson:

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
ST2022   |n|         |u|        |n|
ST2030   |y|         10         |n|
======== =========== ========== ============

.. note:: Function keys are shared with line keys


Yealink
-------

======== =========== ========== ============
Model    Tested [1]_ Fkeys [2]_ XiVO HA [3]_
======== =========== ========== ============
T20P     |n|         2          |n|
T26P     |n|         13         |n|
======== =========== ========== ============

.. note:: Some function keys are shared with line keys


Zenitel
-------

========== =========== ========== ============
Model      Tested [1]_ Fkeys [2]_ XiVO HA [3]_
========== =========== ========== ============
IP station |y|         1          |n|
========== =========== ========== ============

Caption :

.. [1] ``Tested`` means the device has been tested by the XiVO development team and that
       the developers have access to this device.
.. [2] ``Fkeys`` is the number of programmable function keys that you can configure from the
       XiVO web interface. It is not necessarily the same as the number of physical function
       keys the device has (for example, a 6757i has 12 physical keys but you can configure 30
       function keys because of the page system).
.. [3] ``XiVO HA`` means the device is confirmed to work with :ref:`XiVO HA <high-availability>`.
.. [4] These devices are marked as ``Not Tested`` because other similar models using the same firmware have been tested instead.
       If these devices ever present any bugs, they will be troubleshooted by the XiVO support team.

.. |y| replace:: Yes
.. |n| replace:: No
.. |ny| replace:: Not Yet
.. |u| replace:: ---