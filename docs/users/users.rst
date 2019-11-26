.. _users:

Users
=====

.. contents::

WordPress stores the Users in the ``users`` table.

.. _header-n4:

What is a user?
----------------

Each WordPress user has, at the bare minimum, a username, password and
email address.

Once a user account is created, that user may log in using the WordPress
Admin (or programmatically) to access WordPress functions and data.

.. _header-n8:

Roles and Capabilities
-----------------------

Users are assigned :ref:`roles <roles>`, and each role has a set of
:ref:`capabilities <capabilities>`.

You can create new roles with their own set of capabilities.

Custom capabilities can also be created and assigned to existing roles
or new roles.

In WordPress, developers can take advantage of user roles to limit the
set of actions an account can perform.

.. _header-n14:

The Principle of Least Privileges
---------------------------------

WordPress adheres to the principal of least privileges, the practice of
giving a user *only* the privileges that are essential for performing
the desired work.
