.. _options-api:

Options API
===========

.. contents::

The Options API, added in WordPress 1.0, allows creating, reading,
updating and deleting of WordPress options. In combination with the
:ref:`Settings API <settings-api>`
it allows controlling of options defined in settings pages.

.. _header-n4:

Where Options are Stored?
--------------------------

Options are stored in the ``{$wpdb->prefix}_options`` table.
``$wpdb->prefix`` is defined by the ``$table_prefix`` variable set in
the ``wp-config.php`` file.

.. _header-n7:

How Options are Stored?
------------------------

Options may be stored in the WordPress database in one of two ways: as a
single value or as an array of values.

.. _header-n9:

Single Value
~~~~~~~~~~~~~

When saved as a single value, the option name refers to a single value.

.. code-block:: php

   <?php
   // add a new option
   add_option('wporg_custom_option', 'hello world!');
   // get an option
   $option = get_option('wporg_custom_option');

.. _header-n13:

Array of Values
~~~~~~~~~~~~~~~~

When saved as an array of values, the option name refers to an array,
which itself may be comprised key/value pairs.

.. code-block:: php

   <?php
   // array of options
   $data_r = ['title' => 'hello world!', 1, false];
   // add a new option
   add_option('wporg_custom_option', $data_r);
   // get an option
   $options_r = get_option('wporg_custom_option');
   // output the title
   echo esc_html($options_r['title']);

If you are working with a large number of related options, storing them
as an array can have a positive impact on overall performance.

.. note::

    Accessing data as individual options may result in many
    individual database transactions, and as a rule, database
    transactions are expensive operations (in terms of time and server
    resources). When you store or retrieve an array of options, it
    happens in a single transaction, which is ideal.

:ref:`Top ↑ <options-api>`

.. _header-n22:

Function Reference
-------------------

===================== ===================== ======================== ========================
Add Option            Get Option            Update Option            Delete Option
===================== ===================== ======================== ========================
``add_option()``      ``get_option()``      ``update_option()``      ``delete_option()``
``add_site_option()`` ``get_site_option()`` ``update_site_option()`` ``delete_site_option()``
===================== ===================== ======================== ========================
