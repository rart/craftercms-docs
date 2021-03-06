.. _crafter-search-api-search-v2-update-content:

======================
Update Binary Document
======================

Adds a binary document to the Solr index. Internally Solr will use the Tika library to extract
the file content and meta-data. The request should always be a multi-part request, where the
content is sent as a file part.

--------------------
Resource Information
--------------------

+----------------------------+-----------------------------------------------------+
|| HTTP Verb                 || POST                                               |
+----------------------------+-----------------------------------------------------+
|| URL                       || ``/api/2/search/update-content``                   |
+----------------------------+-----------------------------------------------------+
|| Response Formats          || ``JSON``                                           |
+----------------------------+-----------------------------------------------------+

----------
Parameters
----------

+-------------------------+-------------+---------------+----------------------------------------+
|| Name                   || Type       || Required     || Description                           |
+=========================+=============+===============+========================================+
|| index_id               || String     ||              || The index ID                          |
+-------------------------+-------------+---------------+----------------------------------------+
|| site                   || String     || |checkmark|  || The site name                         |
+-------------------------+-------------+---------------+----------------------------------------+
|| id                     || String     || |checkmark|  || The document ID                       |
+-------------------------+-------------+---------------+----------------------------------------+
|| content                || File       || |checkmark|  || Binary file to upload                 |
+-------------------------+-------------+---------------+----------------------------------------+
|| {param}                || String     ||              || Any additional meta-data that needs   |
||                        ||            ||              || to be indexed along with the binary.  |
+-------------------------+-------------+---------------+----------------------------------------+

-------
Example
-------

^^^^^^^
Request
^^^^^^^

.. code-block:: none

  POST .../api/2/search/update-content

.. code-block:: guess

  index_id = editorial
  site = editorial
  id = /site/documents/example.pdf
  content = binary file...

^^^^^^^^
Response
^^^^^^^^

``Status 200 OK``

.. code-block:: json

  {
    "message": "OK"
  }

---------
Responses
---------

+---------+-------------------------------------+------------------------------------------------+
|| Status || Location                           || Response Body                                 |
+=========+=====================================+================================================+
|| 200    || ``.../api/2/search/update-content``|| See example above.                            |
+---------+-------------------------------------+------------------------------------------------+
|| 500    ||                                    || ``{ "message" : "Internal server error" }``   |
+---------+-------------------------------------+------------------------------------------------+
