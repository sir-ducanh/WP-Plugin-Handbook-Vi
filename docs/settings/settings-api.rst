.. _settings-api:

Settings API
============

.. contents::

The Settings API, added in WordPress 2.7, allows admin pages containing
settings forms to be managed semi-automatically. It lets you define
settings pages, sections within those pages and fields within the
sections.

New settings pages can be registered along with sections and fields
inside them. Existing settings pages can also be added to by registering
new settings sections or fields inside of them.

Organizing registration and validation of fields still requires some
effort from developers, but avoids a lot of complex debugging of
underlying options management.

.. warning::

	When using the Settings API, the form POST to
  ``wp-admin/options.php`` which provides fairly strict capabilities
  checking. Users will need the ``manage_options`` capability (and in
  Multisite will have to be a Super Admin) to submit the form.

.. _header-n10:

Why Use the Setting API?
-------------------------

A developer *could* ignore this API and write their own settings page
without it. That begs the question, what benefit does this API bring to
the table? Following is a quick rundown of some of the benefits.

.. _header-n12:

Visual Consistency
~~~~~~~~~~~~~~~~~~~

Using the API to generate your interface elements guarantees that your
settings page will look like the rest of the administrative content.
Your interface will follow the same styleguide and look like it belongs,
and thanks to the talented team of WordPress designers, it’ll look
awesome!

.. _header-n15:

Robustness (Future-Proofing!)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Since the API is part of WordPress Core, any updates will automatically
consider your plugin’s settings page. If you make your own interface
without using Setting API, WordPress Core updates are more likely to
break your customizations. There is also a wider audience testing and
maintaining that API code, so it will tend to be more stable.

.. _header-n18:

Less Work!
~~~~~~~~~~~

Of course the most immediate benefit is that the WordPress API does a
lot of work for you under the hood. Here are a few examples of things
the Settings API does besides applying an awesome-looking, integrated
design.

-  **Handling Form Submissions –** Let WordPress handle retrieving and
   storing your $_POST submissions.

-  **Include Security Measures –** You get extra security measures such
   as nonces, etc. for free.

-  **Sanitizing Data –** You get access to the same methods that the
   rest of WordPress uses for ensuring strings are safe to use.

:ref:`Top ↑ <settings-api>`

.. _header-n28:

Function Reference
------------------

=============================================== ===================================================
Setting Register/Unregister                     Add Field/Section
=============================================== ===================================================
 |``register_setting()``                         |``add_settings_section()``
 |``unregister_setting()``                       |``add_settings_field()``
=============================================== ===================================================

========================================================================= ========================================================================
Options Form Rendering                                                    Errors
========================================================================= ========================================================================
 |``settings_fields()``                                                      | ``add_settings_error()``
 |``do_settings_sections()``                                                 | ``get_settings_errors()``
 |``do_settings_fields()``                                                   |``settings_errors()``
========================================================================= ========================================================================
