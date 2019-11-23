.. _plugin-handbook:

Plugin Handbook
===============

*Welcome to the WordPress Plugin Developer Handbook; are you ready to
jump right in to the world of WordPress plugins?*

The Plugin Developer Handbook is a resource for all things WordPress
plugins. Whether you’re new to WordPress plugin development, or you’re
an experienced plugin developer, you should be able to find the answer
to many of your plugin-related questions right here.

1. If you’re new to plugin development, start by reading the
   :ref:`introduction` and
   then move on to :ref:`plugin-basics`.

2. Section 3 will introduce you to :ref:`security`.

3. :ref:`hooks` are what
   make your plugin interact with WordPress. Learn all about them in
   section 4.

4. To find out more about WordPress’ built-in functionality that you can
   use in your plugin, check out sections 5 – 11: :ref:`administration-menus`,
   :ref:`shortcodes`, :ref:`settings`, :ref:`metadata`, :ref:`post-types`, :ref:`taxonomies`,
   and :ref:`users`.

5. Learn about getting data using the :ref:`http-api` in section
   12.

6. If you’re using :ref:`JavaScript, jQuery or
   Ajax <javascript>` in your
   plugin, you’ll find the information you need in section 13.

7. To learn about time-based WordPress tasks using
   :ref:`Cron <cron>`, check out
   section 14.

8. Sections 15-17 will introduce you to :ref:`internationalizing <internationalization>`
   your plugin, preparing it for :ref:`release on
   WordPress.org <wordpress-org>`,
   and some :ref:`developer
   tools <developer-tools>`
   you might find useful.

The WordPress Plugin Developer Handbook is created by the WordPress
community, for the WordPress community. We are always looking for more
contributors; if you’re interested, stop by the `docs team
blog <https://make.wordpress.org/docs>`__ to find out more about getting
involved.



.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Introduction to Plugin Development

   intro/intro
   intro/what-is-a-plugin




.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Plugin Basics

   plugin-basics/plugin-basics
   plugin-basics/header-requirements
   plugin-basics/including-a-software-license
   plugin-basics/activation-deactivation-hooks
   plugin-basics/uninstall-methods
   plugin-basics/best-practices
   plugin-basics/determining-plugin-and-content-directories
   
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Plugin Security

   security/plugin-security
   security/checking-user-capabilities
   security/data-validation
   security/securing-input
   security/securing-output
   security/nonces




.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Hooks

   hooks/hooks
   hooks/actions
   hooks/filters
   hooks/custom-hooks
   hooks/advanced-topics




.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Privacy

   privacy/privacy
   privacy/suggesting-text-for-the-site-privacy-policy
   privacy/adding-the-personal-data-exporter-to-your-plugin
   privacy/adding-the-personal-data-eraser-to-your-plugin
   privacy/privacy-related-options-hooks-and-capabilities
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Administration Menus

   administration-menus/administration-menus
   administration-menus/top-level-menus
   administration-menus/sub-menus

   
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Shortcodes

   shortcodes/shortcodes
   shortcodes/basic-shortcodes
   shortcodes/enclosing-shortcodes
   shortcodes/shortcodes-with-parameters
   shortcodes/tinymce-enhanced-shortcodes
   
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Settings

   settings/settings
   settings/settings-api
   settings/using-settings-api
   settings/options-api
   settings/custom-settings-page
   
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Metadata

   metadata/metadata
   metadata/managing-post-metadata
   metadata/custom-meta-boxes
   metadata/rendering-post-metadata
   
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Custom Post Types

   post-types/post-types
   post-types/registering-custom-post-types
   post-types/working-with-custom-post-types
   
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Taxonomies

   taxonomies/taxonomies
   taxonomies/working-with-custom-taxonomies
   taxonomies/split-terms-wp-4-2
   
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Users

   users/users
   users/working-with-users
   users/working-with-user-metadata
   users/roles-and-capabilities   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: HTTP API

   http-api/http-api
   
   
   
      
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: JavaScript

   javascript/javascript
   javascript/jquery
   javascript/ajax
   javascript/enqueuing
   javascript/heartbeat-api
   javascript/summary
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Cron

   cron/cron
   cron/understanding-wp-cron-scheduling
   cron/scheduling-wp-cron-events
   cron/hooking-wp-cron-into-the-system-task-scheduler
   cron/simple-testing
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Internationalization

   internationalization/internationalization
   internationalization/localization
   internationalization/how-to-internationalize-your-plugin
   internationalization/security
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: The WordPress.org Plugin Directory

   wordpress-org/wordpress-org
   wordpress-org/detailed-plugin-guidelines
   wordpress-org/planning-your-plugin
   wordpress-org/how-to-use-subversion
   wordpress-org/alerts-and-warnings
   wordpress-org/plugin-developer-faq
   
   
   
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Developer Tools

   developer-tools/developer-tools
   developer-tools/debug-bar-and-add-ons
   developer-tools/helper-plugins
   
   
   
   
