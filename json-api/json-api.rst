registry
========

Get a log of changes to the registry.
-------------------------------------

Client sends::

    {"method" : ["registry","log"]}

Server responds::

    {"log" : [{"commit-id" : "aaa0032234e52673d1b78d757be32a06b8223d86"
              ,"author" : "John Doe <john.doe@example.com>"
              ,"date" : "Sat Feb 7 13:41:03 2015 +0100"
              ,"message" : "Installed Firefox"}]}

Rollback the registry to a previous state.
------------------------------------------

Client sends::

    {"object" : ["registry"]
    ,"method" : "rollback"
    ,"commit-id" : "aaa0032234e52673d1b78d757be32a06b8223d86"}

Server responds::

    {"errors" : nil}

OR::

    {"errors" : ["Commit not found."]}

Update all subuser images
-------------------------

Client sends::

    {"object" : ["registry"]
    ,"method" : "update-all"}

Server responds::

    {"errors" : nil}

NOTE: The server responds instantly, and always says that there are no errors. Use the following command to get the update status:

Client sends::

    {"object" : ["registry"]
    ,"method" : "get-update-status"}

Server responds::

    {"errors" : nil
    ,"output-so-far" : ["Blah blah blah"]
    ,"done" : false}

Verify the consistancy of, and if necesarly repair, the registry
---------------------------

Client sends::

    {"object" : ["registry"]
    ,"method" : "verify"}

Server responds::

    {"errors" : nil}

Lookup an image source based on it's human-readable identifier
--------------------------------------------------------------

Client sends::

    {"object" : ["registry"]
    ,"method" : "lookup-image-source"
    ,"image-source-identifier" : "foo@default"}

Server responds::

    {"errors" : nil
    ,"repository" : "default"
    ,"image-source" : "foo"}

OR::

    {"errors" : ["Image source not found."]}

Subusers
========

Get a list of subusers.
--------------------------

Client sends::

  {"object" : ["registry","subusers"]
   "method" : "list"}

Server responds::

  {"subusers" : ["foo","bar","baz"]}

The server responds with a list of the names of subusers.

Add or reconfigure a subuser.
-----------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "set"
    ,"image-source-identifier" : "foo@default"}

The `image-source-identifier` is the identifier of the image source upon which this subuser is to be based.

Server responds::

    {"errors" : nil}

Delete a subuser
-----------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "delete"}

Server responds::

    {"errors" : nil}

OR::

    {"errors" : ["Subuser does not exist"]}

Get a description of the given subuser.
---------------------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "describe"}

Server responds::

    {"errors" : nil
    ,"description" : "Plain text, user readable, description of subuser"}

OR::

    {"errors" : ["Subuser does not exist"]}

Get subuser's permissions
--------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "get-permissions"}

Server responds::

    {"errors" : nil
    ,"permissions" : <permissions-json-object>}

OR::

    {"errors" : ["Subuser does not exist"]}

Set subuser's permissions
-------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "set-permissions"
    ,"permissions" : <permissions-json-object> }

Server responds::

    {"errors" : nil}

OR::

    {"errors" : ["Subuser does not exist"]}

Get a subuser's image-source
----------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "get-image-source"}

Server responds::

    {"errors" : nil
    ,"source-repo" : "repo-name/id"
    ,"image-source" : "image-source name"}

OR::

    {"errors" : ["Subuser does not exist"]}

Get a subuser's home-dir-on-host
----------------------------------------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "get-home-dir-on-host"}

Server responds::

    {"errors" : nil
    ,"home-dir-on-host" : "/home/user/.subuser/homes/subuser-name"}

OR::

    {"errors" : ["Subuser does not exist"]}

Determine if a subuser is locked(prevented from automatically updating)
------------------------------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "get-locked"}

Server responds::

    {"errors" : nil
    ,"locked" : true}

OR::

    {"errors" : ["Subuser does not exist"]}

Set whether a subuser is locked(from automatically updating)
------------------------------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "set-locked"
    ,"locked" : true}

Server responds::

    {"errors" : nil}

OR::

    {"errors" : ["Subuser does not exist"]}

Determine if a subuser's executable shortcut is installed
-----------------------------------------------------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "get-executable-shortcut-installed"}

Server responds::

    {"errors" : nil
    ,"executable-shortcut-installed" : true}

OR::

    {"errors" : ["Subuser does not exist"]}

Set whether a subuser's executable shortcut is installed
-----------------------------------------------------------------------

Client sends::

    {"object" : ["registry","subusers",<subuser-name>]
    ,"method" : "set-executable-shortcut-installed"
    ,"executable-shortcut-installed" : true}

Server responds::

    {"errors" : nil}

OR::

    {"errors" : ["Subuser does not exist"]}

repositories
============

Get a list of repositories.
---------------------------

Client sends::

  {"object" : ["registry","repositories"]
   "method" : "list"}

Server responds::

  {"repositories" : ["foo","bar","baz"]}

The server responds with a list of the names of repositories.

Add a new repository
--------------------

Client sends::

  {"object" : ["registry","repositories",<repo-name>]
  ,"method" : "create"
  ,"URI" : "https://example.com/repo.git"}

Server responds::

  {"errors" : nil}

Delete an existing repository
-----------------------------

Client sends::

  {"object" : ["registry","repositories",<repo-name>]
  ,"method" : "delete"
  ,"URI" : "https://example.com/repo.git"}

Server responds::

  {"errors" : nil}

OR::

  {"errors" : ["Repository does not exist."]}

Describe a repository
---------------------

Client sends::

  {"object" : ["registry","repositories",<repo-name>]
  ,"method" : "describe"}

Server responds::

  {"errors" : nil
  ,"description" : "User readable plain text description."}

OR::

  {"errors" : ["Repository does not exist."]}

Get a repository's user readable identifier
-------------------------------------------

Client sends::

  {"object" : ["registry","repositories",<repo-name>]
  ,"method" : "get-identifier"}

Server responds::

  {"errors" : nil
  ,"identifier" : "foo@default"}

OR::

  {"errors" : ["Repository does not exist."]}

Determine whether a repository is temporary
-------------------------------------------

Client sends::

  {"object" : ["registry","repositories",<repo-name>]
  ,"method" : "get-temporary"}

Server responds::

  {"errors" : nil
  ,"temporary" : false}

OR::

  {"errors" : ["Repository does not exist."]}

Image-sources within a given repository
=======================================

Get a list of the image sources in a repository
-----------------------------------------------

Client sends::

 {"object" : ["registry","repositories",<repository-name>,"image-sources"]
 "method" : "list"}

Server responds::

  {errors : nil
  ,"image-sources" : ["foo","bar","baz"]}

The server responds with a list of the names of image-sources in the given repository.

OR::

    {"errors" : ["Repository does not exist."]}

Get an image-source's default permissions
-----------------------------------------

Client sends::

 {"object" : ["registry","repositories",<repository-name>,"image-sources",<image-source-name>]
 "method" : "get-permissions"}

Server responds::

  {errors : nil
  ,"permissions" : <permissions-json-object>}

OR::

    {"errors" : ["Repository does not exist."]}

OR::

    {"errors" : ["Image source does not exist."]}

Get a human readable description of an image-source
---------------------------------------------------

Client sends::

 {"object" : ["registry","repositories",<repository-name>,"image-sources",<image-source-name>]
 "method" : "describe"}

Server responds::

  {errors : nil
  ,"description" : "Human readable plain text description of image-source."}

OR::

    {"errors" : ["Repository does not exist."]}

OR::

    {"errors" : ["Image source does not exist."]}

Get a list of an image source's dependencies
--------------------------------------------

Client sends::

 {"object" : ["registry","repositories",<repository-name>,"image-sources",<image-source-name>]
 "method" : "get-dependencies"}

Server responds::

  {errors : nil
  ,"dependencies" : ["foo@default","bar@default"]}

OR::

    {"errors" : ["Repository does not exist."]}

OR::

    {"errors" : ["Image source does not exist."]}

Run the an image-source with default settings for testing purposes
------------------------------------------------------------------

Client sends::

 {"object" : ["registry","repositories",<repository-name>,"image-sources",<image-source-name>]
 ,"method" : "test-run"
 ,"working-directory" : "/home/user/test"
 ,"cli-args" : ["these","are","some","args","to","pass"]}
 
Server responds::

  {errors : nil}

OR::

    {"errors" : ["Repository does not exist."]}

OR::

    {"errors" : ["Image source does not exist."]}

Installed images
================

Remove old unused installed images
----------------------------------

Client sends::

 {"object" : ["installed-images"]
 ,"method" : "remove-old-images"}
 
Server responds::

  {errors : nil}

