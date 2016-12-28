Application Programming Interface
=================================

TODO: document the API using HATEOS pattern (organise by resource subheading, then resource/verb sub-subheading)


Authentication
--------------

Access to the HiPFiSH API is controlled via API tokens. These can be managed via the Web UI.

TODO:
 * insert screen shots and HOWTO for API token management and account management
 * feature specification for API token management and account management
 * would we ever use the API to manage API tokens (how to bootstrap it - would require account creation, credit card etc, the whole thing?)


Archive
-------

One difference between HiPFiSH and a traditional (HTTP/HTTPS) Content Delivery Network is the concept Archive. With a traditional CDN, resources are proxied from an *origin* (or *upstream*). With IPFS, the origin resource may or may not exist, or may or may not be available.

With HiPFiSH, resources are first loaded into the archive, and then they can be served via IPFS.

.. graphviz::

   digraph d {
      archive [shape=rectangle];
      local_file [shape=rectangle];
      post_local;
      post_local -> local_file;
      post_local -> archive;
      http_origin [shape=rectangle];
      post_http;
      post_http -> http_origin;
      post_http -> archive;
      ipfs_origin [shape=rectangle];
      post_ipfs;
      post_ipfs -> ipfs_origin;
      post_ipfs -> archive;
   }

We should have multiple methods to get a file into the archive:
 * POST the file directly
 * POST a URL, which will be subject to a HTTP(S) GET request to pull the file into the archive.
 * POST an IPFS address, which will be subject to a an IPFS GET request to pull the file into the archive.

The first method (POST file) would work with a single file. The other two methods (POST URL/IPFS address) could reasonably work with a (potentially very large) collection of addresses. Conceivably, these collection of addresses could be of mixed type (URLs and IPFS addresses).

All these methods could take some time (non-blocking I/O), so they should immediately return a URL that can be used to check the status status address. For submitted collections of addresses, should it be:
 * a single URL (returning a collection of statuses); or
 * a collection of URLs, (each returning a single status)

The HTTP(S) and IPFS addresses may or may not succeed, due to file availability. So the 


Hosting
-------

TODO:
 * document hosting requirements
 * design hosting API


Search
------

TODO:
 * document search requirements


Statistics
----------

TODO:
 * document statistics requirements
 * design statistics API
 * note similarity and difference to search API (comment elements/paramaters please)


Billing
-------

TODO:
 * document billing requirements
 * design billing API