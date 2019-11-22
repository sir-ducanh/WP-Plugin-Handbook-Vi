.. _header-n0:

Taxonomies
==========

A **Taxonomy** is a fancy word for classifying/grouping of things.
Taxonomies can be hierarchical (with parents/children) or flat.

WordPress stores the Taxonomies in the ``term_taxonomy`` table allowing
developers to register Custom Taxonomies along the ones that already
exist.

Taxonomies have **Terms** which serve as the topic by which you
classify/group things. They are stored inside the ``terms`` table.

E.g. a Taxonomy named “Art” will have multiple Terms; they could be
“Modern” and “18th Century”.

This chapter will show you how to register Custom Taxonomies, how to
retrieve their content from the database, and how to render them to the
public.

--------------

   **Note:** WordPress 3.4 and earlier had a Taxonomy named “Links”
   which was deprecated in WordPress 3.5.

--------------
