.. _split-terms-wp-4-2:

Split Terms (WP 4.2+)
=====================

.. contents::

.. _header-n4:

Prior to WP 4.2
----------------

Prior to WP 4.2, Terms in different Taxonomies with the same slug shared
a single Term ID.

For instance, a Tag and a Category with the slug “news” had the same
Term ID.

.. _header-n8:

WP 4.2+
--------

Beginning with WP 4.2, when one of these shared Terms is updated, it
will be split: the updated term will be assigned a new Term ID.

.. _header-n11:

What does it mean for you?
---------------------------

In the vast majority of situations, this update will be seamless and
uneventful. However, some plugins and themes who store Term IDs in
options, post meta, user meta, or elsewhere might be affected.

.. _header-n14:

Handling the Split
-------------------

WP 4.2 includes two different tools to help authors of plugins and
themes with the transition.

.. _header-n16:

The ``split_shared_term`` hook
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When a shared term is assigned a new Term ID, a new
``split_shared_term`` action is fired.

Here are a few examples of how plugin and theme authors can leverage
this hook to ensure that stored Term IDs are updated.

.. _header-n19:

Term ID stored in an option
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let’s say your plugin stores an option called ``featured_tags`` that
contains an array of Term IDs (``[4, 6, 10]``) that serve as the query
parameter for your homepage featured posts section.

In this example, you’ll hook to ``split_shared_term`` action, check
whether the updated Term ID is in the array, and update if necessary.

.. code-block:: php

   /**
    * Update featured_tags option when a shared term gets split.
    *
    * @param int $term_id ID of the formerly shared term.
    * @param int $new_term_id ID of the new term created for the $term_taxonomy_id.
    * @param int $term_taxonomy_id ID for the term_taxonomy row affected by the split.
    * @param string $taxonomy Taxonomy for the split term.
    */
   function wporg_featured_tags_split($term_id, $new_term_id, $term_taxonomy_id, $taxonomy)
   {
       // we only care about tags, so we'll first verify that the taxonomy is post_tag.
       if ($taxonomy === 'post_tag') {

           // get the currently featured tags.
           $featured_tags = get_option('featured_tags');

           // if the updated term is in the array, note the array key.
           $found_term = array_search($term_id, $featured_tags);
           if ($found_term !== false) {

               // the updated term is a featured tag! replace it in the array, save the new array.
               $featured_tags[$found_term] = $new_term_id;
               update_option('featured_tags', $featured_tags);
           }
       }
   }
   add_action('split_shared_term', 'wporg_featured_tags_split', 10, 4);

.. _header-n24:

Term ID stored in post meta
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let’s say your plugin stores a Term ID in post meta for pages so that
you can show related posts for a certain page.

In this case, you need to use the
`get_posts() <https://developer.wordpress.org/reference/functions/get_posts/>`__
function to get the pages with your ``meta_key`` and a update the
``meta_value`` matching the split term ID.

.. code-block:: php

   /**
    * Update related posts term ID for pages
    *
    * @param int $term_id ID of the formerly shared term.
    * @param int $new_term_id ID of the new term created for the $term_taxonomy_id.
    * @param int $term_taxonomy_id ID for the term_taxonomy row affected by the split.
    * @param string $taxonomy Taxonomy for the split term.
    */
   function wporg_page_related_posts_split($term_id, $new_term_id, $term_taxonomy_id, $taxonomy)
   {
       // find all the pages where meta_value matches the old term ID.
       $page_ids = get_posts([
                                 'post_type'  => 'page',
                                 'fields'     => 'ids',
                                 'meta_key'   => 'meta_key',
                                 'meta_value' => $term_id,
                             ]);

       // if such pages exist, update the term ID for each page.
       if ($page_ids) {
           foreach ($page_ids as $id) {
               update_post_meta($id, 'meta_key', $new_term_id, $term_id);
           }
       }
   }
   add_action('split_shared_term', 'wporg_page_related_posts_split', 10, 4);

.. _header-n29:

The ``wp_get_split_term`` function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

      Using the ``split_shared_term`` hook is the preferred method for processing Term ID changes.

      However, there may be cases where Terms are split without your plugin having a chance to hook to the ``split_shared_term`` action.

WP 4.2 stores information about Taxonomy Terms that have been split, and
provides the
`wp_get_split_term() <https://developer.wordpress.org/reference/functions/wp_get_split_term/>`__
utility function to help developers retrieve this information.

Consider the case above, where your plugin stores Term IDs in an
option named ``featured_tags``.
You may want to build a function that validates these tag IDs (perhaps
to be run on plugin update), to be sure that none of the featured tags
has been split:

.. code-block:: php

   function wporg_featured_tags_check_split()
   {
       $featured_tag_ids = get_option('featured_tags', []);

       // check to see whether any IDs correspond to post_tag terms that have been split.
       foreach ($featured_tag_ids as $index => $featured_tag_id) {
           $new_term_id = wp_get_split_term($featured_tag_id, 'post_tag');

           if ($new_term_id) {
               $featured_tag_ids[$index] = $new_term_id;
           }
       }

       // save
       update_option('featured_tags', $featured_tag_ids);
   }

Note that
`wp_get_split_term() <https://developer.wordpress.org/reference/functions/wp_get_split_term/>`__
takes two parameters, ``$old_term_id`` and ``$taxonomy`` and returns an
integer.

If you need to retrieve a list of all split terms associated with an old
Term ID, regardless of taxonomy, use
`wp_get_split_terms() <https://developer.wordpress.org/reference/functions/wp_get_split_terms/>`__.
