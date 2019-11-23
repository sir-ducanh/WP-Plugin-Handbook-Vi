.. _best-practices:

Best Practices
==============

.. contents::

Here are some best practices to help organize your code so it works well
alongside WordPress core and other WordPress plugins.

.. _header-n4:

Avoid Naming Collisions
-----------------------

A naming collision happens when your plugin is using the same name for a
variable, function or a class as another plugin.

Luckily, you can avoid naming collisions by using the methods below.

.. _header-n7:

Procedural 
~~~~~~~~~~~

By default, all variables, functions and classes are defined in the
**global namespace**, which means that it is possible for your plugin to
override variables, functions and classes set by another plugin and
vice-versa. Variables that are defined *inside*\ of functions or classes
are not affected by this.

.. _header-n9:

Prefix Everything 
^^^^^^^^^^^^^^^^^^

All variables, functions and classes should be prefixed with a unique
identifier. Prefixes prevent other plugins from overwriting your
variables and accidentally calling your functions and classes. It will
also prevent you from doing the same.

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n12:

Check for Existing Implementations 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

PHP provides a number of functions to verify existence of variables,
functions, classes and constants. All of these will return true if the
entity exists.

-  **Variables**:
   `isset() <http://php.net/manual/en/function.isset.php>`__ (includes
   arrays, objects, etc.)

-  **Functions**:
   `function_exists() <http://php.net/manual/en/function.function-exists.php>`__

-  **Classes**:
   `class_exists() <http://php.net/manual/en/function.class-exists.php>`__

-  **Constants**:
   `defined() <http://php.net/manual/en/function.defined.php>`__

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n24:

Example 
^^^^^^^^

.. code:: php

   //Create a function called "wporg_init" if it doesn't already exist
   if ( !function_exists( 'wporg_init' ) ) {
   	function wporg_init() {
       register_setting( 'wporg_settings', 'wporg_option_foo' );
     }
   } 

   //Create a function called "wporg_get_foo" if it doesn't already exist
   if ( !function_exists( 'wporg_get_foo' ) ) {
     function wporg_get_foo() {
       return get_option( 'wporg_option_foo' );
     }
   }

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n28:

OOP 
~~~~

An easier way to tackle the naming collision problem is to use a
`class <http://php.net/manual/en/language.oop5.php>`__ for the code of
your plugin.

You will still need to take care of checking whether the name of the
class you want is already taken but the rest will be taken care of by
PHP.

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n32:

Example 
^^^^^^^^

.. code:: php

   if ( !class_exists( 'WPOrg_Plugin' ) ) {
   	class WPOrg_Plugin  
   	{
   		public static function init() {
         register_setting( 'wporg_settings', 'wporg_option_foo' );
       }
       
       public static function get_foo() {
       	return get_option( 'wporg_option_foo' );
       }
     }
     
     WPOrg_Plugin::init();
     WPOrg_Plugin::get_foo();
   }

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n35:

File Organization 
------------------

The root level of your plugin directory should contain your
``plugin-name.php`` file and, optionally, your
`uninstall.php <https://developer.wordpress.org/plugin/the-basics/uninstall-methods/>`__
file. All other files should be organized into sub folders whenever
possible.

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n38:

Folder Structure 
~~~~~~~~~~~~~~~~~

A clear folder structure helps you and others working on your plugin
keep similar files together.

Here’s a sample folder structure for reference:

.. code:: 

   /plugin-name
        plugin-name.php
        uninstall.php
        /languages
        /includes
        /admin
             /js
             /css
             /images
        /public
             /js
             /css
             /images

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n43:

Plugin Architecture 
--------------------

The architecture, or code organization, you choose for your plugin will
likely depend on the size of your plugin.

For small, single-purpose plugins that have limited interaction with
WordPress core, themes or other plugins, there’s little benefit in
engineering complex classes; unless you know the plugin is going to
expand greatly later on.

For large plugins with lots of code, start off with classes in mind.
Separate style and scripts files, and even build-related files. This
will help code organization and long-term maintenance of the plugin.

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n48:

Conditional Loading 
~~~~~~~~~~~~~~~~~~~~

It’s helpful to separate your admin code from the public code. Use the
conditional
`is_admin() <https://codex.wordpress.org/Function_Reference/is_admin>`__.

For example:

.. code:: php

   if ( is_admin() ) {
   	// we are in admin mode
   	require_once( dirname( __FILE__ ) . '/admin/plugin-name-admin.php' );
   }

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n53:

Architecture Patterns 
~~~~~~~~~~~~~~~~~~~~~~

While there are a number of possible architecture patterns, they can
broadly be grouped into three variations:

-  `Single plugin file, containing
   functions <https://github.com/GaryJones/move-floating-social-bar-in-genesis/blob/master/move-floating-social-bar-in-genesis.php>`__

-  `Single plugin file, containing a class, instantiated object and
   optionally
   functions <https://github.com/norcross/wp-comment-notes/blob/master/wp-comment-notes.php>`__

-  `Main plugin file, then one or more class
   files <https://github.com/tommcfarlin/WordPress-Plugin-Boilerplate>`__

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n63:

Architecture Patterns Explained 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Specific implementations of the more complex of the above code
organizations have already been written up as tutorials and slides:

-  `Slash – Singletons, Loaders, Actions, Screens,
   Handlers <https://jjj.blog/2012/12/slash-architecture-my-approach-to-building-wordpress-plugins/>`__

-  `Implementing the MVC Pattern in WordPress
   Plugins <http://iandunn.name/wp-mvc>`__

`Top
↑ <https://developer.wordpress.org/plugins/plugin-basics/best-practices/#top>`__

.. _header-n71:

Boilerplate Starting Points 
----------------------------

Instead of starting from scratch for each new plugin you write, you may
want to start with a **boilerplate**. One advantage of using a
boilerplate is to have consistency among your own plugins. Boilerplates
also make it easier for other people to contribute to your code if you
use a boilerplate they are already familiar with.

These also serve as further examples of different yet comparable
architectures.

-  `WordPress Plugin
   Boilerplate <https://github.com/tommcfarlin/WordPress-Plugin-Boilerplate>`__:
   A foundation for WordPress Plugin Development that aims to provide a
   clear and consistent guide for building your plugins.

-  `WordPress Plugin
   Bootstrap <https://github.com/claudiosmweb/wordpress-plugin-boilerplate>`__:
   Basic bootstrap to develop WordPress plugins using Grunt, Compass,
   GIT, and SVN.

-  `WP Skeleton
   Plugin <https://github.com/ptahdunbar/wp-skeleton-plugin>`__:
   Skeleton plugin that focuses on unit tests and use of composer for
   development.

-  `WP CLI
   Scaffold <https://developer.wordpress.org/cli/commands/scaffold/plugin/>`__:
   The Scaffold command of WP CLI creates a skeleton plugin with options
   such as CI configuration files

Of course, you could take different aspects of these and others to
create your own custom boilerplate.
