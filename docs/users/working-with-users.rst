.. _working-with-users:

Working with Users
==================

.. contents::

.. _header-n4:

Adding Users
-------------

To add a user you can use
`wp_create_user() <https://developer.wordpress.org/reference/functions/wp_create_user/>`__
or
`wp_insert_user() <https://developer.wordpress.org/reference/functions/wp_insert_user/>`__.

`wp_create_user() <https://developer.wordpress.org/reference/functions/wp_create_user/>`__
creates a user using only the username, password and email parameters
while while
`wp_insert_user() <https://developer.wordpress.org/reference/functions/wp_insert_user/>`__
accepts an array or object describing the user and it’s properties.

.. _header-n7:

Create User
~~~~~~~~~~~~

.. code-block:: php

   wp_create_user(
       string $username,
       string $password,
       string $email = ''
   );

Allows you to create a new WordPress user.

.. note::

    It uses `wp_slash() <https://developer.wordpress.org/reference/functions/wp_slash/>`__
    to escape the values. The PHP compact() function to create an array with these values. The
    `wp_insert_user() <https://developer.wordpress.org/reference/functions/wp_insert_user/>`__
    to perform the insert operation.

Please refer to the Function Reference about
`wp_create_user() <https://developer.wordpress.org/reference/functions/wp_create_user/>`__
for full explanation about the used parameters.

.. _header-n15:

Example Create
^^^^^^^^^^^^^^^

.. code-block:: php

   // check if the username is taken
   $user_id = username_exists($user_name);

   // check that the email address does not belong to a registered user
   if (!$user_id && email_exists($user_email) === false) {
   // create a random password
       $random_password = wp_generate_password(
           $length = 12,
           $include_standard_special_chars = false
       );
   // create the user
       $user_id = wp_create_user(
           $user_name,
           $random_password,
           $user_email
       );
   }

:ref:`Top ↑ <working-with-users>`

.. _header-n18:

Insert User
~~~~~~~~~~~~

.. code-block:: php

   wp_insert_user(
       array|object|WP_User $userdata
   );

.. note::

     The function calls a filter for most predefined properties.

     The function performs the action ``user_register`` when creating a
     user (user ID does not exist).

     The function performs the action ``profile_update`` when updating the
     user (user ID exists).

Please refer to the Function Reference about
`wp_insert_user() <https://developer.wordpress.org/reference/functions/wp_insert_user/>`__
for full explanation about the used parameters.

.. _header-n28:

Example Insert
^^^^^^^^^^^^^^^

Below is an example showing how to insert a new user with the website
profile field filled in.

.. code-block:: php

   $username = $_POST['username'];
   $password = $_POST['password'];
   $website = $_POST['website'];
   $user_data = [
       'user_login' => $username,
       'user_pass'  => $password,
       'user_url'   => $website,
   ];

   $user_id = wp_insert_user($user_data);

   // success
   if (!is_wp_error($user_id)) {
       echo 'User created: ' . $user_id;
   }

:ref:`Top ↑ <working-with-users>`

.. _header-n32:

Updating Users
---------------

.. code-block:: php

   wp_update_user(
       mixed $userdata
   );

Updates a single user in the database. The update data is passed along
in the $userdata array/object.

To update a single piece of user meta data, use
`update_user_meta() <https://developer.wordpress.org/reference/functions/update_user_meta/>`__
instead.
To create a new user, use
`wp_insert_user() <https://developer.wordpress.org/reference/functions/wp_insert_user/>`__
instead.

.. note::

    If current user’s password is being updated, then the cookies will be cleared!



Please refer to the Function Reference about
`wp_update_user() <https://developer.wordpress.org/reference/functions/wp_update_user/>`__
for full explanation about the used parameters.

:ref:`Top ↑ <working-with-users>`

.. _header-n42:

Example Update
~~~~~~~~~~~~~~~

Below is an example showing how to update a user’s website profile
field.

.. code-block:: php

   $user_id = 1;
   $website = 'https://wordpress.org';

   $user_id = wp_update_user(
       [
           'ID'       => $user_id,
           'user_url' => $website,
       ]
   );

   if (is_wp_error($user_id)) {
       // error
   } else {
       // success
   }

.. _header-n46:

Deleting Users
---------------

.. code-block:: php

   wp_delete_user(
       int $id,
       int $reassign = null
   );

Delete the user and optionally reassign associated entities to another
user ID.

.. note::

    The function performs the action ``deleted_user`` after the user have been deleted.


.. warning::

    If the $reassign parameter is not set to a valid user
    ID, then all entities belonging to the deleted user will be deleted!

Please refer to the Function Reference about
`wp_delete_user() <https://developer.wordpress.org/reference/functions/wp_delete_user/>`__
for full explanation about the used parameters.
