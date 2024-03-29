.. _roles-and-capabilities:

Roles and Capabilities
======================

.. contents::

Roles and capabilities are two important aspects of WordPress that allow
you to control user privileges.

WordPress stores the Roles and their Capabilities in the ``options``
table under the ``user_roles`` key.

.. _header-n5:

.. _roles:

Roles
------

A role defines a set of capabilities for a user. For example, what the
user may see and do in his dashboard.

**By default, WordPress have six roles:**

-  Super Admin

-  Administrator

-  Editor

-  Author

-  Contributor

-  Subscriber

More roles can be added and the default roles can be removed.

.. figure:: https://developer.wordpress.org/files/2014/09/wp-roles.png
   :alt:

.. _header-n23:

Adding Roles
~~~~~~~~~~~~~

Add new roles and assign capabilities to them with
`add_role() <https://developer.wordpress.org/reference/functions/add_role/>`__.

.. code-block:: php

   function wporg_simple_role() {
       add_role(
           'simple_role',
           'Simple Role',
           [
               'read'         => true,
               'edit_posts'   => true,
               'upload_files' => true,
           ]
       );
   }

   // Add the simple_role.
   add_action('init', 'wporg_simple_role');


.. warning::

	     After the first call to `add_role() <https://developer.wordpress.org/reference/functions/add_role/>`__

       Sequential calls will do nothing: including altering the capabilities list, which might not be the behavior that you’re expecting.



.. note::

      To alter the capabilities list in bulk: remove the role using `remove_role() <https://developer.wordpress.org/reference/functions/remove_role/>`__
      and add it again using `add_role() <https://developer.wordpress.org/reference/functions/add_role/>`__ with the new capabilities.

      Make sure to do it only if the capabilities differ from what you’re expecting (i.e. condition this) or you’ll degrade performance considerably!

.. _header-n38:

Removing Roles
~~~~~~~~~~~~~~~

Remove roles with
`remove_role() <https://developer.wordpress.org/reference/functions/remove_role/>`__.

.. code-block:: php

   function wporg_simple_role_remove() {
       remove_role( 'simple_role' );
   }

   // Remove the simple_role.
   add_action( 'init', 'wporg_simple_role_remove' );


.. warning::

	     After the first call to `remove_role() <https://developer.wordpress.org/reference/functions/remove_role/>`__,
       the Role and it’s Capabilities will be removed from the database!

       Sequential calls will do nothing.


.. note::

	   If you’re removing the default roles:

     -  We advise **against** removing the Administrator and Super Admin roles!

     -  Make sure to keep the code in your plugin/theme as future WordPress updates may add these roles again.

     -  Run ``update_option('default_role', YOUR_NEW_DEFAULT_ROLE)`` since you’ll be deleting ``subscriber`` which is WP’s default role.




:ref:`Top ↑ <roles-and-capabilities>`

.. _header-n60:

.. _capabilities:

Capabilities
-------------

Capabilities define what a **role** can and can not do: edit posts,
publish posts, etc.

.. note::

	   Custom post types can require a certain set of Capabilities.

.. _header-n67:

Adding Capabilities
~~~~~~~~~~~~~~~~~~~~

You may define new capabilities for a role.

Use
`get_role() <https://developer.wordpress.org/reference/functions/get_role/>`__
to get the role object, then use the ``add_cap()`` method of that object
to add a new capability.

.. code-block:: php

   function wporg_simple_role_caps() {
       // Gets the simple_role role object.
       $role = get_role( 'simple_role' );

       // Add a new capability.
       $role->add_cap( 'edit_others_posts', true );
   }

   // Add simple_role capabilities, priority must be after the initial role definition.
   add_action( 'init', 'wporg_simple_role_caps', 11 );


.. note::

	   It’s possible to add custom capabilities to any role.

     Under the default WordPress admin, they would have no effect, but they can be used for custom admin screen and front-end areas.

.. _header-n77:

Removing Capabilities
~~~~~~~~~~~~~~~~~~~~~~

You may remove capabilities from a role.

The implementation is similar to Adding Capabilities with the difference
being the use of ``remove_cap()`` method for the role object.

.. _header-n81:

Using Roles and Capabilities
-----------------------------

.. _header-n83:

Get Role
~~~~~~~~~

Get the role object including all of it’s capabilities with
`get_role() <https://developer.wordpress.org/reference/functions/get_role/>`__.

.. code-block:: php

    get_role( $role );

.. _header-n87:

User Can
~~~~~~~~~

Check if a user have a specified **role** or **capability** with
`user_can() <https://developer.wordpress.org/reference/functions/user_can/>`__.

.. code-block:: php

   user_can( $user, $capability );


.. warning::

      There is an undocumented, third argument, $args, that may include the object against which the test should be performed.

      E.g. Pass a post ID to test for the capability of that specific post.

.. _header-n98:

Current User Can
~~~~~~~~~~~~~~~~~

`current_user_can() <https://developer.wordpress.org/reference/functions/current_user_can/>`__
is a wrapper function for
`user_can() <https://developer.wordpress.org/reference/functions/user_can/>`__
using the current user object as the ``$user`` parameter.

Use this in scenarios where back-end and front-end areas should require
a certain level of privileges to access and/or modify.

.. code:: php

   current_user_can( $capability );

`Top
↑ <https://developer.wordpress.org/plugins/users/roles-and-capabilities/#top>`__

.. _header-n103:

Example
~~~~~~~~

Here’s a practical example of adding an Edit link on the in a template
file if the user has the proper capability:

.. code:: php

   if ( current_user_can( 'edit_posts' ) ) {
       edit_post_link( esc_html__( 'Edit', 'wporg' ), '<p>', '</p>');
   }

`Top
↑ <https://developer.wordpress.org/plugins/users/roles-and-capabilities/#top>`__

.. _header-n107:

Multisite
----------

The
`current_user_can_for_blog() <https://developer.wordpress.org/reference/functions/current_user_can_for_blog/>`__
function is used to test if the current user has a certain **role** or
**capability** on a specific blog.

.. code:: php

   current_user_can_for_blog( $blog_id, $capability );

`Top
↑ <https://developer.wordpress.org/plugins/users/roles-and-capabilities/#top>`__

.. _header-n111:

Reference
----------

Codex Reference for `User Roles and
Capabilities <https://wordpress.org/support/article/roles-and-capabilities/>`__.
