.. _planning-your-plugin:

Planning, Submitting, and Maintaining Plugins
=============================================

.. contents::

You’ve written the next `Hello
Dolly <https://wordpress.org/plugins/hello-dolly/>`__ and you want the
world to use it. What should you do?

.. _header-n4:

1. Test once and test again 
----------------------------

With any luck, your plugin will be used by lots of people in many
different situations and hosting environments. You’ll want to make sure
you’ve tested your plugin to make sure it works in any situation and
doesn’t frustrate your users.

`Top
↑ <https://developer.wordpress.org/plugins/wordpress-org/planning-your-plugin/#top>`__

.. _header-n7:

2. Pick a good name 
--------------------

A plugin name should reflect the uniqueness of you and your work. When
you pick a name, make sure you’re not violating trademarks or stomping
on someone else’s product names. If you’re not working for Facebook, you
shouldn’t name your plugin ‘Facebook’s Dancing Squirrels’ after all. A
much better name would be ‘Dancing Squirrels for Facebook’ for example.
It can be hard to come up with a good name, so take your time. Your
plugin URL cannot be changed after you submit it, but the display name
can change a thousand times.

Display names are generated from the headers in the main plugin file so
mind your Ps and Qs.

`Top
↑ <https://developer.wordpress.org/plugins/wordpress-org/planning-your-plugin/#top>`__

.. _header-n11:

3. Write great documentation 
-----------------------------

A `README.txt <https://wordpress.org/plugins/developers/#readme>`__ file
is the best place to start, as it’s a standard reference point for all
plugins. You’ll want to make sure you include:

-  A concise description of what your plugin actually does. If it does a
   lot, it might be better as two plugins.

-  Installation instructions, especially if there’s special
   configuration to be done. If a user needs to register with your
   service, make sure you link to it.

-  Directions on how to get support, and what you do and do not support.

`Top
↑ <https://developer.wordpress.org/plugins/wordpress-org/planning-your-plugin/#top>`__

.. _header-n21:

4. Submit your plugin 
----------------------

In order to submit a plugin, there are three steps:

1. Register on WordPress.org with a valid, regularly checked email
   address. If you are submitting a plugin on behalf of a company, use
   an **official** company email for verification.

2. Whitelist ``plugins@wordpress.org`` in your email client to ensure
   you receive email communications.

3. `Submit your
   plugin <https://wordpress.org/plugins/developers/add/>`__ with a
   brief overview of what it does and a complete, ready to go, zip of
   the plugin. The zip must be the complete version of your plugin, just
   like you would use to manually upload via the plugin installer.

Once a plugin is queued for review, we will review the code for any
issues within 14 business days. Most of the issues can be avoided by
following the guidelines. If we do find issues, we will contact the
developer(s), and work towards a resolution. Once approved, you’ll
receive an email with details as to how to access to a `Subversion
Repository <https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/>`__
where you’ll store your plugin.

After you upload your plugin (and a `readme
file <https://wordpress.org/plugins/developers/#readme>`__) in that
repository via SVN, it will appear on the `plugin
directory <https://wordpress.org/plugins/>`__.

`Top
↑ <https://developer.wordpress.org/plugins/wordpress-org/planning-your-plugin/#top>`__

.. _header-n33:

5. Push out the first version 
------------------------------

The WordPress.org plugins directory is the easiest way for potential
users to download and install your plugin. WordPress’ integration with
the plugin directory means your plugin can be updated by the user in a
couple of clicks.

When you’re ready to release your first version, you’ll want to `sign
up <https://wordpress.org/plugins/add/>`__. After a review process is
completed successfully, you’ll be granted a Subversion Repository for
your code. The WordPress.org site has good documentation for `making
your first Subversion
commits <https://developer.wordpress.org/plugin/wordpress-org/deploying-your-plugin/>`__
and `the overall
process <https://developer.wordpress.org/plugins/wordpress-org/>`__.

`Top
↑ <https://developer.wordpress.org/plugins/wordpress-org/planning-your-plugin/#top>`__

.. _header-n37:

6. Embrace open source 
-----------------------

Open source is one of the most powerful ideas of our time because it
empowers collaboration across borders. By encouraging contributions,
you’re allowing others to love your code as much as you do. There are
several options to open source your code:

-  `Github <http://github.com/>`__ makes it simple to get others
   involved with your project. Other developers and users can submit bug
   fixes or reports, feature requests, or brand new contributions
   easily. Github has a `great documentation
   portal <https://help.github.com/>`__ and even an `interactive
   demo <http://try.github.com/>`__ if you’ve never used Git before.

-  `Bitbucket <https://bitbucket.org/>`__ is an alternative to Github
   with similar features.

-  The WordPress.org Plugin Directory provides and requires you to use a
   `Subversion
   repository <https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/>`__.

`Top
↑ <https://developer.wordpress.org/plugins/wordpress-org/planning-your-plugin/#top>`__

.. _header-n47:

7. Listen to your users
-----------------------

You’ll often find that your users put your code through many more test
cases than you could’ve imagined. This can be tremendously valuable
feedback.

Releasing your code through WordPress.org means your plugin
automatically has a support forum. Use it! You can subscribe to receive
new posts by email and respond to your users in a timely manner. They
just want to love your plugin as much as you do.

Andrew Spittle, a Happiness Engineer at Automattic, has a couple good
posts on providing support: “\ `Avoiding
Easy <http://andrewspittle.net/2012/01/31/avoiding-easy/>`__\ ” and
“\ `The Speed of
Support <http://andrewspittle.net/2012/04/18/the-speed-of-support/>`__.”
Jetpack also has a post you can point to about `writing great bug
reports <http://jetpack.me/2011/11/18/how-to-write-a-great-bug-report/>`__.

`Top
↑ <https://developer.wordpress.org/plugins/wordpress-org/planning-your-plugin/#top>`__

.. _header-n52:

8. Regularly push new versions 
-------------------------------

The best plugins are the ones that keep iterating over time, pushing
small changes along the way. Don’t let your hard work go stale by
waiting too long to update. Keep in mind, constant upgrades can cause
‘Update Fatigue’ and users will stop upgrading. Keeping a balance
between too few updates and too many updates is important.

`Top
↑ <https://developer.wordpress.org/plugins/wordpress-org/planning-your-plugin/#top>`__

.. _header-n55:

9. Rinse and repeat 
--------------------

Like in other parts of life, the best things come from patience and hard
work.
