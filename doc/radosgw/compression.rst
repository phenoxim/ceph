===========
Compression
===========

.. versionadded:: Kraken

The Ceph Object Gateway supports server-side compression of uploaded objects,
using any of Ceph's existing compression plugins.


Configuration
=============

Compression can be enabled on a Zone as part of `Multisite Configuration`::

  $ radosgw-admin zone modify --rgw-zone=default --rgw-zonegroup=default --compression=<type>

The compression ``type`` refers to the name of the compression plugin to use
when writing new object data. Each compressed object remembers which plugin
was used, so changing this setting does not hinder the ability to decompress
existing objects, not does it force existing objects to be recompressed.

This compression setting applies globally to all new objects uploaded,
regardless of their bucket or user. Compression can be disabled by setting
the ``type`` to an empty string or ``none``.

.. note:: A ``default`` zone and zonegroup are created for you if you have
   not done any previous Multisite Configuration.


Metrics
=======

While all existing commands and APIs continue to report object and bucket
sizes based their uncompressed data, compression metrics for a given bucket
are available in the fields ``size_utilized`` and ``size_kb_utilized`` from::

  $ radosgw-admin bucket stats --bucket=<name>


.. _`Multisite Configuration`: ../../multisite
