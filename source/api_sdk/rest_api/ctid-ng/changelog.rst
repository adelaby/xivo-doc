.. _ctid_ng_changelog:

*******************************
xivo-ctid-ng HTTP API changelog
*******************************

17.05
=====

* New attribute ``is_caller`` for Call objects in routes:

  * ``GET,POST /calls``
  * ``GET /calls/{call_id}``
  * ``GET,POST /users/me/calls``

17.03
=====

* New routes for switchboard operations. This is not (yet) related to the current switchboard
  implementation.

  * ``GET /1.0/switchboards/{switchboard_uuid}/calls/held``
  * ``PUT /1.0/switchboards/{switchboard_uuid}/calls/held/{call_id}``
  * ``PUT /1.0/switchboards/{switchboard_uuid}/calls/held/{call_id}/answer``

17.02
=====

* A new API for switchboard operations. This is not (yet) related to the current switchboard
  implementation.

  * ``GET /1.0/switchboards/{switchboard_uuid}/calls/queued``
  * ``PUT /1.0/switchboards/{switchboard_uuid}/calls/queued/{call_id}/answer``

17.01
=====

* A new parameter for call creation (``POST /calls`` and ``POST /users/me/calls``)

  * ``from_mobile``

16.16
=====

* A new API for managing voicemails messages:

    * GET ``/1.0/voicemails/{voicemail_id}``
    * GET ``/1.0/voicemails/{voicemail_id}/folders/{folder_id}``
    * DELETE ``/1.0/voicemails/{voicemail_id}/messages/{message_id}``
    * GET ``/1.0/voicemails/{voicemail_id}/messages/{message_id}``
    * PUT ``/1.0/voicemails/{voicemail_id}/messages/{message_id}``
    * POST ``/1.0/voicemails/{voicemail_id}/messages/{message_id}/recording``
    * GET ``/1.0/users/me/voicemails``
    * GET ``/1.0/users/me/voicemails/folders/{folder_id}``
    * DELETE ``/1.0/users/me/voicemails/messages/{message_id}``
    * GET ``/1.0/users/me/voicemails/messages/{message_id}``
    * PUT ``/1.0/users/me/voicemails/messages/{message_id}``
    * POST ``/1.0/users/me/voicemails/messages/{message_id}/recording``

* A new ``timeout`` parameter has been added to the following URL:

    * POST ``/1.0/transfers``
    * POST ``/1.0/users/me/transfers``

* A new ``line_id`` parameter has been added to the following URL:

    * POST ``/1.0/calls``
    * POST ``/1.0/users/me/calls``


16.11
=====

* A new API for getting the status of lines:

    * GET ``/1.0/lines/{id}/presences``


16.10
=====

* A new API for checking the status of the daemon:

    * GET ``/1.0/status``


16.09
=====

* A new API for updating user presences:

    * GET ``/1.0/users/{uuid}/presences``
    * PUT ``/1.0/users/{uuid}/presences``
    * GET ``/1.0/users/me/presences``
    * PUT ``/1.0/users/me/presences``

* New APIs for listing and hanging up calls of a user:

    * GET ``/1.0/users/me/calls``
    * DELETE ``/1.0/users/me/calls/{id}``

* New APIs for listing, cancelling and completing transfers of a user:

    * GET ``/1.0/users/me/transfers``
    * DELETE ``/1.0/users/me/transfers/{transfer_id}``
    * PUT ``/1.0/users/me/transfers/{transfer_id}/complete``

* POST ``/1.0/users/me/transfers`` may now return 403 status code.
* Originates (POST ``/*/calls``) now return 400 if an invalid extension is given.


16.08
=====

* A new API for making calls from the authenticated user:

    * POST ``/1.0/users/me/calls``

* A new API for sending chat messages:

    * POST ``/1.0/chats``
    * POST ``/1.0/users/me/chats``

* A new parameter for transfer creation (POST ``/1.0/transfers``):

    * ``variables``

* A new API for making transfers from the authenticated user:

    * POST ``/1.0/users/me/transfers``
