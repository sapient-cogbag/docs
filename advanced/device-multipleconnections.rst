.. _multiple-connections:

multipleConnections
===================

.. versionadded:: TBD

``multipleConnections`` is an advanced device setting that affects
connection handling. The default is zero, equivalent to *one*: only one
connection is maintained to the device.

If you set this to a value greater than one, multiple connections will be
maintained to the device. Multiple connections can yield improved
performance by load-balancing traffic over multiple physical links.

.. note::

    Incoming connections exceeding the configured number will be rejected,
    thus this setting must be applied symmetrically. That is if you
    configure device A to use four connections to B, you must also configure
    B to use four connections to A.

.. note::

    Additional connections are established over time, roughly at the rate of
    one per minute when Syncthing is in a steady state, so you may not see
    the expected number of connections immediately after changing this
    setting.

Load Balancing
--------------

When there are multiple connections between two devices, one connection is
dedicated to metadata transmission: index updates, changes to folder pause
status, etc. Requests and responses are sent over the other connections
randomly. The number of connections in the GUI is represented as `1 + n` for
this reason, e.g. if you configure four connections, the GUI will show `1 +
3` to indicate one metadata connection and three data connections.

Rate Limiting
-------------

Device rate limiting applies to the aggregate of all connections, regardless
of the number of connections. The limit is not per connection.

Connection Types
----------------

Both TCP and QUIC connections are supported for multiple connections.
Syncthing will, however, only keep connections with the best priority; by
default, TCP has better priority than QUIC, so establishing a TCP connection
will cause existing QUIC connections to be closed. Connection priorities can
be configured.

Multiple connections cannot be established over relays.
