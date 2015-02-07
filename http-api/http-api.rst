Class hierarchy
%%%%%%%%%%%%%%%

.. warning:: The HTTP API is a workin in progress and has not been implemented anywhere yet!

The class hierarchy is designed to reflect the class hierarchy of the code in subuserlib.  Resource names are intentionally similar to method names. However, while method names are imperitive, resource names are declarative. For example, the method ``Repository.isTemporary()`` becomes the resource ``/registry/repositories/{repository}/temporary``.

/registry
=========

``GET /registry/log``
---------------------

Get a log of changes to the registry.

``PUT /registry/rollback``
--------------------------

Rollback the registry to a previous state.



/registry/subusers
==================

``GET /registry/subusers``
--------------------------

Get a list of subusers.

This request takes no query parameters.

  ===========      ======
  Status code      Status
  ===========      ======
  200              OK
  ===========      ======
 
Body:

A JSON list of strings. Each string is the name of a subuser.

``PUT /registry/subusers/{subuser-name}``
-----------------------------------------

Add or reconfigure a subuser.

Query parameters

  =========                  ====
  Parameter                  Description
  =========                  ====
  image-source-identifier    The identifier of the image source upon which this subuser is to be based.
  =========                  ====

``DELETE /registry/subusers/{subuser-name}``
--------------------------------------------

``GET /registry/subusers/{subuser-name}/description``
-----------------------------------------------------

Get a description of the given subuser.

This request takes no query parameters.

  ===========      ======
  Status code      Status
  ===========      ======
  200              OK
  404              Subuser does not exist
  ===========      ======

Body:

A plain text description of the given subuser.
 

``GET /registry/subusers/{subuser-name}/permissions``
-----------------------------------------------------

``PUT /registry/subusers/{subuser-name}/permissions``
-----------------------------------------------------

``GET /registry/subusers/{subuser-name}/image-source``
------------------------------------------------------

``GET /registry/subusers/{subuser-name}/home-dir-on-host``
----------------------------------------------------------

``GET /registry/subusers/{subuser-name}/locked``
------------------------------------------------

``PUT /registry/subusers/{subuser-name}/locked``
------------------------------------------------

``GET /registry/subusers/{subuser-name}/executable-shortcut-installed``
-----------------------------------------------------------------------

``PUT /registry/subusers/{subuser-name}/executable-shortcut-installed``
-----------------------------------------------------------------------


/registry/repositories
======================

``GET /registry/repositories``
------------------------------

Get a list of repositories.

This request takes no query parameters.

  ===========      ======
  Status code      Status
  ===========      ======
  200              OK
  ===========      ======
 
Body:

A JSON list of strings. Each string is the name of a repository.

``PUT /registry/repositories/{repository-name}``
------------------------------------------------

``DELETE /registry/repositories/{repository-name}``
---------------------------------------------------

``GET /registry/repositories/{repository-name}/description``
------------------------------------------------------------

``GET /registry/repositories/{repository-name}/display-name``
-------------------------------------------------------------

``GET /registry/repositories/{repository-name}/temporary``
----------------------------------------------------------

/registry/repositories/{repository}/image-sources
=================================================

``GET /registry/repositories/{repository-name}/image-sources``
--------------------------------------------------------------

Get a list of image-sources.

This request takes no query parameters.

  ===========      ======
  Status code      Status
  ===========      ======
  200              OK
  ===========      ======
 
Body:

A JSON list of strings. Each string is the name of an image-source.

``GET /registry/repositories/{repository-name}/image-sources/{image-source-name}/permissions``
----------------------------------------------------------------------------------------------

``GET /registry/repositories/{repository-name}/image-sources/{image-source-name}/description``
----------------------------------------------------------------------------------------------

``GET /registry/repositories/{repository-name}/image-sources/{image-source-name}/dependencies``
-----------------------------------------------------------------------------------------------


RPC
%%%

Running subusers
================

``PUT /rpc/subuser/run``
------------------------

Lookup
======

``GET /rpc/image-source``
----------------------------

Look up the image source given an image source identifier.

Query parameters

  =========                  =========
  Parameter                  Meaning
  =========                  =========
  image-source-identifier    The identifier of the image source to be looked up.
  =========                  =========

Responce codes

  ===========      ======
  Status code      Status
  ===========      ======
  200              OK
  400              Malformed image Id
  ===========      ======

When the status is ``200``, the responce body is a plain text URL to the image source.

Ex::

    GET /rpc/image-source
    image-source-identifier: iceweasel@default
   

    Gives:

    /repositories/default/image-sources/iceweasel

Development
===========

``PUT /rpc/image-source/test``
---------------------------

Test the given image-source. 

Query parameters

  =========          ===
  Parameter          Description
  =========          ===
  image-source-path  Path to the image source to be tested
  working-directory  The working directory which may be inherited by the test subuser
  cli-args           The CLI args to be passed to the test subuser (JSON list)
  =========          ===


``PUT /rpc/subuser/dry-run``
----------------------------

Maintenance
============

``PUT /rpc/maintenance/update``
---------------------------

Update all subuser images

``PUT /rpc/maintenance/remove-old-images``
--------------------------------------

``PUT /rpc/maintenance/verify``
---------------------------

