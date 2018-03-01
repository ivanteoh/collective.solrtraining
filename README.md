Plone / Solr integration training
=================================

in .buildout/default.cfg
[buildout]
eggs-directory = /Users/ivan/buildout-cache/eggs
download-cache = /Users/ivan/buildout-cache/download

./bin/buildout -No install solr-instance

Simple way is to update the config as `indexed:false`

https://pypi.python.org/pypi/collective.indexing/2.0b1 will integrate into
Plone 5.1 to make collective.solr easier

Set one or both of the following options in the Solr server configuration via the collective.recipe.solrinstance buildout recipe:

    autoCommitMaxDocs - The number of updates that have occurred since the last commit.
    autoCommitMaxTime - The number of milliseconds since the oldest uncommitted update.
is good for both case `Synchronous immediately` and `Synchronous batched`

`Asynchronous` have no control if something wrong in Solr server. If you do use it,
`Clear Solr Index` and `Clearup Solr Index` for time to time.

collective.solr only support single core at the moment.

How many "News Item" articles are in the demo Solr?
18 (portal_type:"News Item")

How many "Documents" were created between 14 October 2016 and Today?
16 (+portal_type:"Document" +created:[2016-10-14T00:00:00Z TO NOW])

How many Items have No description
4 (-Description:[* TO *])

How many Items have a title starting with "Lore*"
6 (Title:Lore*)

What's the Date and Portal Type of the Item created first and containing "Lorem"
http://86.119.38.69:8983/solr/collection1/select?q=SearchableText%3ALorem&sort=Date+asc&rows=1&fl=portal_type%3ADate&wt=json&indent=true

Exercise Facets: a list of all portal types with count
http://86.119.38.69:8983/solr/collection1/select?q=*%3A*&sort=Date+asc&wt=json&indent=true&facet=true&facet.field=portal_type

Facet navigation will use collective.solr for optimaise

In order to index plomino catalog, have to look in to collective.indexing. it will included in the core in 5.1

On suggestion section,
below are the right urls:
http://localhost:8080/Plone/@@suggest-terms?term=plone&wt=json
http://localhost:8983/solr/spell?q=Plone&wt=json

On fancy search section:
http://localhost:8080/Plone/@@training-fancysearch

Books
=====

https://www.packtpub.com/big-data-and-business-intelligence/apache-solr-enterprise-search-server-third-edition

https://cwiki.apache.org/confluence/display/solr/Language+Analysis
