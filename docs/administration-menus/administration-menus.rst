.. _administration-menus:

Administration Menus
====================

Administration Menus are the interfaces displayed in WordPress
Administration. They allow you to add option pages for your plugin.

.. note::
  For information on managing **Navigation Menus**, see
  the :ref:`Navigation Menus <navigation-menus>`
  chapter of the `Theme Developer Handbook <https://developer.wordpress.org/theme/>`__.

.. _header-n8:

Top-Level Menus and Sub-Menus
-----------------------------

The Top-level menus are rendered along the left side of the WordPress
Administration. Each menu may contain a set of Sub-menus.

When deciding between :ref:`Top-level menus <top-level-menus>`
and :ref:`Sub-menus <sub-menus>`
think carefully about the needs of your plugin as well as the needs of
your end users.

.. warning:: We recommend developers with a single option page to add
   it as Sub-menu to one of the existing Top-level menus; such as
   *Settings* or *Tools*.
