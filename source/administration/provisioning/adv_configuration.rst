**********************
Advanced Configuration
**********************

.. _dhcp-integration:

DHCP Integration
================

If your phones are getting their network configuration from your XiVO's DHCP server,
it's possible to activate the DHCP integration on the
:menuselection:`Configuration --> Provisioning --> General` page.

What DHCP integration does is that, on every DHCP request made by one of your
phones, the DHCP server sends information about the request to ``provd``, which
can then use this information to update its device database.

This feature is useful for phones which lack information in their TFTP/HTTP
requests. For example, without DHCP integration, it's impossible to extract
model information for phones from the Cisco 7900 series. Without the model
information extracted, there's chance your device won't be automatically
associated to the best plugin.

This feature can also be useful if your phones are not always getting the same IP
addresses, for one reason or another. Again, this is useful only for some phones,
like the Cisco 7900; it has no effect for Aastra 6700.


Creating Custom Templates
=========================

Custom templates comes in handy when you have some really specific configuration
to make on your telephony devices.

Templates are handled on a per plugin basis. It's not possible for a template to be
shared by more than one plugin since it's a design limitation of the plugin system
of ``provd``.

.. note::
   When you install a new plugin, templates are not migrated automatically, so you must
   manually copy them from the old plugin directory to the new one. This does not apply for a plugin upgrade.

Let's suppose we have installed the ``xivo-aastra-3.3.1-SP2`` plugin and
want to write some custom templates for it.

First thing to do is to go into the directory where the plugin is installed::

   cd /var/lib/xivo-provd/plugins/xivo-aastra-3.3.1-SP2

Once you are there, you can see there's quite a few files and directories::

   tree
   .
   +-- common.py
   +-- entry.py
   +-- pkgs
   |   +-- pkgs.db
   +-- plugin-info
   +-- README
   +-- templates
   |   +-- 6730i.tpl
   |   +-- 6731i.tpl
   |   +-- 6739i.tpl
   |   +-- 6753i.tpl
   |   +-- 6755i.tpl
   |   +-- 6757i.tpl
   |   +-- 9143i.tpl
   |   +-- 9480i.tpl
   |   +-- base.tpl
   +-- var
       +-- cache
       +-- installed
       +-- templates
       +-- tftpboot
           +-- Aastra
               +-- aastra.cfg

The interesting directories are:

templates
   This is where the original templates lies. You *should not* edit these files
   directly but instead copy the one you want to modify in the var/templates directory.

var/templates
   This is the directory where you put and edit your custom templates.

var/tftpboot
   This is where the configuration files lies once they have been generated from the templates.
   You should look at them to confirm that your custom templates are giving you the result you are expecting.

.. warning::
   When you uninstall a plugin, the plugin directory is removed altogether, including all the custom templates.

A few things to know before writing your first custom template:

* templates use the `Jinja2 template engine <http://jinja.pocoo.org/docs/templates/>`_.
* when doing an ``include`` or an ``extend`` from a template, the file is first looked up
  in the :file:`var/templates` directory and then in the :file:`templates` directory.
* device in autoprov mode are affected by templates, because from the point of view
  of ``provd``, there's no difference between a device in autoprov mode or fully configured.
  This means there's usually no need to modify static files in :file:`var/tftpboot`. And this
  is a bad idea since a plugin upgrade will override these files.


Custom template for every devices
---------------------------------

::

   cp templates/base.tpl var/templates
   vi var/templates/base.tpl
   provd_pycli -c 'devices.using_plugin("xivo-aastra-3.3.1-SP2").reconfigure()'

Once this is done, if you want to synchronize all the affected devices, use the following command::

    provd_pycli -c 'devices.using_plugin("xivo-aastra-3.3.1-SP2").synchronize()'


Custom template for a specific model
------------------------------------

Let's supose we want to customize the template for our 6739i::

   cp templates/6739i.tpl var/templates
   vi var/templates/6739i.tpl
   provd_pycli -c 'devices.using_plugin("xivo-aastra-3.3.1-SP2").reconfigure()'


Custom template for a specific device
-------------------------------------

To create a custom template for a specific device you have to create a device-specific template
named :file:`<device_specific_file_with_extension>.tpl` in the :file:`var/templates/` directory :

* for an Aastra phone, if you want to customize the file :file:`00085D2EECFB.cfg` you will have
  to create a template file named :file:`00085D2EECFB.cfg.tpl`,
* for a Snom phone, if you want to customize the file :file:`000413470411.xml` you will have
  to create a template file named :file:`000413470411.xml.tpl`,
* for a Polycom phone, if you want to customize the file :file:`0004f2211c8b-user.cfg` you will have
  to create a template file named :file:`0004f2211c8b-user.cfg.tpl`,
* and so on.

Here, we want to customize the content of a device-specific file named :file:`00085D2EECFB.cfg`,
we need to create a template named :file:`00085D2EECFB.cfg.tpl`::

   cp templates/6739i.tpl var/templates/00085D2EECFB.cfg.tpl
   vi var/templates/00085D2EECFB.cfg.tpl
   provd_pycli -c 'devices.using_mac("00085D2EECFB").reconfigure()'

.. note::
   The choice to use this syntax comes from the fact that ``provd`` supports devices that do not have MAC addresses,
   namely softphones.

   Also, some devices have more than one file (like Snom), so this way make
   it possible to customize more than 1 file.

The template to use as the base for a device specific template will vary depending on the need.
Typically, the model template will be a good choice, but it might not always be the case.


Changing the Plugin Used by a Device
====================================

From time to time, new firmwares are released by the devices manufacturer.
This sometimes translate to a new plugin being available for these devices.

When this happens, it almost always means the new plugin obsoletes the older one.
The older plugin is then considered "end-of-life", and won't receive any new updates
nor be available for new installation.

Let's suppose we have the old ``xivo-aastra-3.2.2.1136`` plugin installed on our
xivo and want to use the newer ``xivo-aastra-3.3.1-SP2`` plugin.

Both these plugins can be installed at the same time, and you can manually change
the plugin used by a phone by editing it via the :menuselection:`Services --> IPBX --> Devices`
page.

If you are using custom templates in your old plugin, you should copy
them to the new plugin and make sure that they are still compatible.

Once you take the decision to migrate all your phones to the new plugin, you can
use the following command::

   provd_pycli -c 'helpers.mass_update_devices_plugin("xivo-aastra-3.2.2.1136", "xivo-aastra-3.3.1-SP2")'

Or, if you also want to synchronize (i.e. reboot) them at the same time::

   provd_pycli -c 'helpers.mass_update_devices_plugin("xivo-aastra-3.2.2.1136", "xivo-aastra-3.3.1-SP2", synchronize=True)'

You can check that all went well by looking at the :menuselection:`Services --> IPBX --> Devices`
page.


NAT
===

The provisioning server has partial support for environment where the telephony devices are behind a
`NAT`_ equipment.

.. _NAT: http://en.wikipedia.org/wiki/NAT

By default, each time the provisioning server receives an HTTP/TFTP request from a device, it makes
sure that only one device has the source IP address of the request. This is not a desirable
behaviour when the provisioning server is used in a NAT environment, since in this case, it's normal
that more than 1 devices have the same source IP address (from the point of view of the server).

If *all* your devices used on your XiVO are behind a NAT, you should disable this behaviour by
setting the ``NAT`` option to 1 via the :menuselection:`Configuration --> Provisioning --> General`
page.

Enabling the NAT option will also improve the performance of the provisioning server in this scenario.

Limitations
-----------

* You must only have phones of the following brands:

  * Aastra
  * Cisco SPA

* All your devices must be behind a NAT equipment (the devices may be grouped behind different NAT
  equipments, not necessarily the same one)
* You must provision the devices via the Web interface, i.e. associate the devices from the user
  form. Using the 6-digit provisioning code on the phone will produce unexpected results (i.e. the
  wrong device will be provisioned)

For technical information about why other devices are not supported, you can look at `this issue
<https://projects.xivo.io/issues/5107>`_  on the XiVO bug tracker.
