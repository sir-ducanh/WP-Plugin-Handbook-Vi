.. _managing-post-metadata:

Managing Post Metadata
======================

.. contents::

.. _header-n4:

Adding Metadata
----------------

Adding metadata can be done quite easily with
`add_post_meta() <https://developer.wordpress.org/reference/functions/add_post_meta/>`__.
The function accepts a ``post_id``, a ``meta_key``, a ``meta_value``,
and a ``unique`` flag.

The ``meta_key`` is how your plugin will reference the meta value
elsewhere in your code. Something like ``mycrazymetakeyname`` would
work, however a prefix related to your plugin or theme followed by a
description of the key would be more useful. ``wporg_featured_menu``
might be a good one. It should be noted that the same ``meta_key`` may
be used multiple times to store variations of the metadata (see the
unique flag below).

The ``meta_value`` can be a string, integer, or an array. If it’s an
array, it will be automatically serialized before being stored in the
database.

The ``unique`` flag allows you to declare whether this key should be
unique. A **non** unique key is something a post can have multiple
variations of, like price.
If you only ever want **one** price for a post, you should flag it
``unique`` and the ``meta_key`` will have one value only.

.. _header-n10:

Updating Metadata
------------------

If a key already exists and you want to update it, use
`update_post_meta() <https://developer.wordpress.org/reference/functions/update_post_meta/>`__.
If you use this function and the key does **NOT** exist, then it will
create it, as if you’d used
`add_post_meta() <https://developer.wordpress.org/reference/functions/add_post_meta/>`__.

Similar to
`add_post_meta() <https://developer.wordpress.org/reference/functions/add_post_meta/>`__,
the function accepts a ``post_id``, a ``meta_key``, a ``meta_value``,
and a ``unique`` flag.

.. _header-n14:

Deleting Metadata
------------------

`delete_post_meta() <https://developer.wordpress.org/reference/functions/delete_post_meta/>`__
takes a ``post_id``, a ``meta_key``, and optionally ``meta_value``. It
does exactly what the name suggests.

.. _header-n17:

Character Escaping
-------------------

Post meta values are passed through the
`stripslashes() <http://php.net/manual/en/function.stripslashes.php>`__
function upon being stored, so you will need to be careful when passing
in values (such as JSON) that might include \\ escaped characters.

Consider the JSON value ``{"key":"value with \"escaped quotes\""}``:

.. code-block:: php

   $escaped_json = '{"key":"value with \"escaped quotes\""}';
   update_post_meta($id, 'escaped_json', $escaped_json);
   $broken = get_post_meta($id, 'escaped_json', true);
   /*
   $broken, after stripslashes(), ends up unparsable:
   {"key":"value with "escaped quotes""}
   */

.. _header-n21:

Workaround
~~~~~~~~~~~

By adding one more level of \\ escaping using the function
`wp_slash() <https://developer.wordpress.org/reference/functions/wp_slash/>`__
(introduced in WP 3.6), you can compensate for the call to
`stripslashes() <http://php.net/manual/en/function.stripslashes.php>`__:

.. code-block:: php

   $escaped_json = '{"key":"value with \"escaped quotes\""}';
   update_post_meta($id, 'double_escaped_json', wp_slash($escaped_json));
   $fixed = get_post_meta($id, 'double_escaped_json', true);
   /*
   $fixed, after stripslashes(), ends up as desired:
   {"key":"value with \"escaped quotes\""}
   */

.. _header-n25:

Hidden Custom Fields
---------------------

If you are a plugin or theme developer and you are planning to use
custom fields to store parameters, it is important to note that
WordPress will not show custom fields which have ``meta_key`` starting
with an “_” (underscore) in the custom fields list on the post edit
screen or when using the `the_meta()<https://developer.wordpress.org/reference/functions/the_meta/>`__
template function.

This can be useful in order to show these custom fields in an unusual
way by using the
`add_meta_box() <https://developer.wordpress.org/reference/functions/add_meta_box/>`__
function.

The example below will add a unique custom field with the ``meta_key``
name ‘_color’ and the ``meta_value`` of ‘red’ but this custom field
will not display in the post edit screen:

.. code-block:: php

   add_post_meta(68, '_color', 'red', true);


.. _header-n31:

Hidden Arrays
~~~~~~~~~~~~~~

In addition, if the ``meta_value`` is an array, it will not be displayed
on the page edit screen, even if you don’t prefix the ``meta_key`` name
with an underscore.
