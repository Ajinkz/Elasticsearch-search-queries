# Elasticsearch-search-queries

Write search request API to search request against one or more clusters of Elasticsearch

## Searching using the query parameter

`GET /<index>/_search`

`POST /<index>/_search`

`GET /_search`

`POST /_search`

## Search a specific index

`curl -GET "localhost:9200/customers/_search?q=wyoming&pretty"`

## Search in several indices

`curl -GET "localhost:9200/customers,products/_search?q=user:wyoming&pretty"`

## Search in all indices

`curl -X GET "localhost:9200/_search?q=name:kimchy&pretty"`

OR

`curl -X GET "localhost:9200/_all/_search?q=name:kimchy&pretty"`

OR

`curl -X GET "localhost:9200/*/_search?q=name:kimchy&pretty"`

## Multi search API
Executes several searches with a single API request

`GET /<index>/_msearch`

```	
GET /twitter/_msearch
{ }
{"query" : {"match" : { "message": "this is a test"}}}
{"index": "twitter2"}
{"query" : {"match_all" : {}}}
```

Create payload name requests
```
$ cat requests
{"index" : "test"}
{"query" : {"match_all" : {}}, "from" : 0, "size" : 10}
{"index" : "test", "search_type" : "dfs_query_then_fetch"}
{"query" : {"match_all" : {}}}
{}
{"query" : {"match_all" : {}}}

{"query" : {"match_all" : {}}}
{"search_type" : "dfs_query_then_fetch"}
{"query" : {"match_all" : {}}}
```

Query using curl

`$ curl -H "Content-Type: application/x-ndjson" -XGET localhost:9200/_msearch --data-binary "@requests"; echo
`

