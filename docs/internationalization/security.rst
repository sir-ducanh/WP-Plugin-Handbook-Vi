.. _header-n0:

Internationalization Security
=============================

.. contents::

Security is often overlooked when talking about internationalization,
but there are a few important things to keep in mind.

.. _header-n4:

Check for Spam and Other Malicious Strings 
-------------------------------------------

When a translator submits a localization to you, always check to make
sure they didn’t include spam or other malicious words in their
translation. You can use `Google
Translate <https://translate.google.com/>`__ to translate their
translation back into your native language so that you can easily
compare the original and translated strings.

`Top
↑ <https://developer.wordpress.org/plugins/internationalization/security/#top>`__

.. _header-n7:

Escape Internationalized Strings 
---------------------------------

You can’t trust that a translator will only add benign text to their
localization; if they want to, they could add malicious JavaScript or
other code instead. To protect against that, it’s important to treat
internationalized strings like you would any other untrusted input.

If you’re outputting the strings, then they should be escaped.

   Insecure:

.. code:: php

   <?php _e( 'The REST API content endpoints were added in WordPress 4.7.', 'your-text-domain' ); ?>

..

   Secure:

.. code:: php

   <?php esc_html_e( 'The REST API content endpoints were added in WordPress 4.7.', 'your-text-domain' ); ?>

Alternatively, some people choose to rely on a translation verification
mechanism, rather than adding escaping to their code. One example of a
verification mechanism is `the editor
roles <https://make.wordpress.org/polyglots/handbook/glossary/#project-translation-editor>`__
that the WordPress Polyglots team uses for
`translate.wordpress.org <https://translate.wordpress.org/>`__. This
ensures that any translation submitted by an untrusted contributor has
been verified by a trusted editor before being accepted.

`Top
↑ <https://developer.wordpress.org/plugins/internationalization/security/#top>`__

.. _header-n18:

Use Placeholders for URLs 
--------------------------

Don’t include URLs in internationalized strings, because a malicious
translator could change them to point to a different URL. Instead, use
placeholders for
`printf() <http://php.net/manual/en/function.printf.php>`__ or
`sprintf() <http://us3.php.net/manual/en/function.sprintf.php>`__.

   Insecure:

.. code:: php

   <?php _e(
       'Please <a href="https://wordpress.org/support/register.php">
        register for a WordPress.org account</a>.',
       'your-text-domain'
   ); ?>

..

   Secure:

.. code:: php

   <?php printf(
       __(
           'Please <a href="%s">register for a WordPress.org account</a>.',
           'your-text-domain'
       ),
       'https://wordpress.org/support/register.php'
   ); ?>

`Top
↑ <https://developer.wordpress.org/plugins/internationalization/security/#top>`__

.. _header-n27:

Compile Your Own .mo Binaries
-----------------------------

Often translators will send the compiled .mo file along with the
plaintext .po file, but you should discard their .mo file and compile
your own, because you have no way of knowing whether or not it was
compiled from the corresponding .po file, or a different one. If it was
compiled against a different one, then it could contain spam and other
malicious strings without your knowledge.

Using PoEdit to generate the binary will override the headers in the .po
file, so instead it’s better to compile it from the command line:

.. code:: php

   msgfmt -cv -o /path/to/output.mo /path/to/input.po
