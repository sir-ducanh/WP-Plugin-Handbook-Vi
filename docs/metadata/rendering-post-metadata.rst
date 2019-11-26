.. _rendering-post-metadata:

Rendering Post Metadata
=======================

There are two functions that allow easy access to metadata stored in the
``postmeta`` table:
`get_post_meta() <https://developer.wordpress.org/reference/functions/get_post_meta/>`__,
`get_post_custom() <https://developer.wordpress.org/reference/functions/get_post_custom/>`__.

Please see the function reference on parameter details.

.. code-block:: php

   get_post_meta(
       int $post_id,
       string $key = '',
       bool $single = false
   );

Example:

.. code-block:: php

   $wporg_meta_value = get_post_meta(get_the_ID(), 'wporg_meta_key');

Please see the function reference on parameter details.

.. code-block:: php

   get_post_custom(
       int $post_id
   );

Example:

.. code-block:: php

   $meta_array = get_post_custom(get_the_ID());
