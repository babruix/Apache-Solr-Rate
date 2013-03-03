Description
----------------

This module integrates the Rate voting results with Apache Solr sorting.
You could visit Administration » Configuration » Search and metadata » Apache Solr search » Settings (or admin/config/search/apachesolr/settings) to change the result scoring, or 
add variable 'apachesolr_rate_boost' to your settings.php, for example:
$conf['apachesolr_rate_boost'] = '4:200.0';
Value should be string, containing two variables: one is for vote steepness and second one is for vote_boost.

When Solr indexing documents, function apachesolr_rate_apachesolr_index_document_build_node() will be called.
After fetching voting results for current node it saves data into ApacheSolrDocument field fs_rating_result.

Before search is going to be executed, function apachesolr_rate_apachesolr_query_alter() field fs_rating_result will be retrived from solr.
Then fetched current boost settings: values for vote steepness and vote_boost.  
For boost formula is used expression:  recip(rord(fs_rating_result), $vote_steepness, $total, $total) ^ $vote_boost

Then this expression added to the query as "bf" query parameter.


Original Author
---------------
Moshe Weitzman <weitzman AT tejasa.com>


Current Maintainer
------------------
Alexey Romanov <romanalexey AT gmail.com>