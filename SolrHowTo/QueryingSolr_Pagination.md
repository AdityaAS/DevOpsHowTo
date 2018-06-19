###Pagination
* When the collections are really large, iteration using the standard start, rows parameters is highly inefficient. Cursors make the search / iteration much much faster.

* Code to query solr collection using cursors: [https://github.com/ubleipzig/solrdump](https://github.com/ubleipzig/solrdump)
* [Great introduction] Official Docs: [https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html](https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html)