.. _mail_configuration:

****
Mail
****

.. index:: mail

This section describes how to configure the mail server shipped with XiVO (Postfix) and the way XiVO handles mails.

In :menuselection:`Configuration --> Network --> Mail`, the following options can be configured:

* :guilabel:`Domain Name messaging` : the server's displayed domain. Will appear in "Received" mail headers.
* :guilabel:`Source address of the server` : domain part of headers "Return-Path" and "From".
* :guilabel:`Relay SMTP` and :guilabel:`FallBack relay SMTP` : relay mail servers.
* :guilabel:`Rewriting shipping addresses` : Canonical address Rewriting. See `Postfix canonical documentation <http://www.postfix.org/ADDRESS_REWRITING_README.html#canonical>`_ for more info.

.. warning::
   Postfix, the mail server shipped with XiVO, should be stopped on an installed XiVO with no valid and reachable DNS servers configured. If Postfix is not stopped, messages will bounce in queues and could end up affecting core pbx features.

If you need to disable Postfix here is how you should do it::

     systemctl stop postfix
     systemctl disable postfix

If you ever need to enable Postfix again::

    systemctl enable postfix
    systemctl start postfix

Alternatively, you can empty Postfix's queues by issuging the following commands on the XiVO server::

    postsuper -d ALL
