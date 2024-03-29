.. _plugin-basics:

Plugin Basics
=============

.. contents::

.. _header-n3:

Getting Started
---------------

At its simplest, a WordPress plugin is a PHP file with a WordPress
plugin header comment. It’s highly recommended that you create a
directory to hold your plugin so that all of your plugin’s files are
neatly organized in one place.

To get started creating a new plugin, follow the steps below.

1. Navigate to the WordPress installation’s **wp-content** directory.

2. Open the **plugins** directory.

3. Create a new directory and name it after the plugin (e.g.
   ``plugin-name``).

4. Open the new plugin’s directory.

5. Create a new PHP file (it’s also good to name this file after your
   plugin, e.g. ``plugin-name.php``).

Here’s what the process looks like on the Unix command line:

.. code-block:: shell

  wordpress$ cd wp-content
  wp-content$ cd plugins
  plugins$ mkdir plugin-name
  plugins$ cd plugin-name
  plugin-name$ vi plugin-name.php

In the example above, “vi” is the name of the text editor. Use whichever
editor that is comfortable for you.

Now that you’re editing your new plugin’s PHP file, you’ll need to add a
**plugin header comment**. This is a specially formatted PHP block
comment that contains metadata about the plugin, such as its name,
author, version, license, etc. The plugin header comment must comply
with the :ref:`header requirements <header-requirements>`,
and at the very least, contain the **name** of the plugin.

Only **one file** in the plugin’s folder should have the header comment
— if the plugin has multiple PHP files, only one of those files should
have the header comment.

.. code-block:: php

  <?php
  /**
   * Plugin Name: YOUR PLUGIN NAME
   */


After you save the file, you should be able to see your plugin listed in
your WordPress site. Log in to your WordPress site, and click
**Plugins** on the left navigation pane of your WordPress Admin. This
page displays a listing of all the plugins your WordPress site has. Your
new plugin should now be in that list!

.. _header-n25:

Hooks: Actions and Filters
--------------------------

WordPress hooks allow you to tap into WordPress at specific points to
change how WordPress behaves without editing any core files.

There are two types of hooks within WordPress: *actions* and *filters*.
Actions allow you to add or change WordPress functionality, while
filters allow you to alter content as it is loaded and displayed to the
website user.

Hooks are not just for plugin developers; hooks are used extensively to
provide default functionality by WordPress core itself. Other hooks are
unused place holders that are simply available for you to tap into when
you need to alter how WordPress works. This is what makes WordPress so
flexible.

.. _header-n29:

Basic Hooks
~~~~~~~~~~~

The 3 basic hooks you’ll need when creating a plugin are the
`register_activation_hook() <https://developer.wordpress.org/reference/functions/register_activation_hook/>`__,
the
`register_deactivation_hook() <https://developer.wordpress.org/reference/functions/register_deactivation_hook/>`__,
and the
`register_uninstall_hook() <https://developer.wordpress.org/reference/functions/register_uninstall_hook/>`__.

The :ref:`activation hook <activation-deactivation-hooks>` is run when you *activate* your plugin. You would use this to provide a
function to set up your plugin — for example, creating some default
settings in the ``options`` table.

The :ref:`deactivation hook <activation-deactivation-hooks>`
is run when you *deactivate* your plugin. You would use this to provide
a function that clears any temporary data stored by your plugin.

These :ref:`uninstall methods <uninstall-methods>`
are used to clean up after your plugin is *deleted* using the WordPress
Admin. You would use this to delete all data created by your plugin,
such as any options that were added to the ``options`` table.

.. _header-n35:

Adding Hooks
~~~~~~~~~~~~

You can add your own, custom hooks with
`do_action() <https://developer.wordpress.org/reference/functions/do_action/>`__,
which will enable developers to extend your plugin by passing functions
through your hooks.

.. _header-n38:

Removing Hooks
~~~~~~~~~~~~~~

You can also use invoke
`remove_action() <https://developer.wordpress.org/reference/functions/remove_action/>`__
to remove a function that was defined earlier. For example, if your
plugin is an add-on to another plugin, you can use
`remove_action() <https://developer.wordpress.org/reference/functions/remove_action/>`__
with the same function callback that was added by the previous plugin
with
`add_action() <https://developer.wordpress.org/reference/functions/add_action/>`__.
The priority of actions is important in these situations, as
`remove_action() <https://developer.wordpress.org/reference/functions/remove_action/>`__
would need to run after the initial
`add_action() <https://developer.wordpress.org/reference/functions/add_action/>`__.

You should be careful when removing an action from a hook, as well as
when altering priorities, because it can be difficult to see how these
changes will affect other interactions with the same hook. We highly
recommend testing frequently.

You can learn more about creating hooks and interacting with them in the
:ref:`Hooks <hooks>` section of
this handbook.

.. _header-n43:

WordPress APIs
--------------

Did you know that WordPress provides a number of `Application
Programming Interfaces
(APIs) <https://make.wordpress.org/core/handbook/core-apis/>`__? These
APIs can greatly simplify the code you need to write in your plugins.
You don’t want to reinvent the wheel, especially when so many people
have done a lot of the work and testing for you.

The most common one is the `Options
API <https://codex.wordpress.org/Options_API>`__, which makes it easy to
store data in the database for your plugin. If you’re thinking of using
`cURL <https://en.wikipedia.org/wiki/CURL>`__ in your plugin, the `HTTP
API <https://codex.wordpress.org/HTTP_API>`__ might be of interest to
you.

Since we’re talking about plugins, you’ll want to study the `Plugin
API <https://codex.wordpress.org/Plugin_API>`__. It has a variety of
functions that will assist you in developing plugins.

.. _header-n48:

How WordPress Loads Plugins
---------------------------

When WordPress loads the list of installed plugins on the Plugins page
of the WordPress Admin, it searches through the ``plugins`` folder (and
its sub-folders) to find PHP files with WordPress plugin header
comments. If your entire plugin consists of just a single PHP file, like
`Hello Dolly <https://wordpress.org/plugins/hello-dolly/>`__, the file
could be located directly inside the root of the ``plugins`` folder. But
more commonly, plugin files will reside in their own folder, named after
the plugin.

.. _header-n51:

Sharing your Plugin
-------------------

Sometimes a plugin you create is just for your site. But many people
like to share their plugins with the rest of the WordPress community.
Before sharing your plugin, one thing you need to do is `choose a
license <https://opensource.org/licenses/category>`__. This lets the
user of your plugin know how they are allowed to use your code. To
maintain compatibility with WordPress core, it is recommended that you
pick a license that works with GNU General Public License (GPLv2+).
