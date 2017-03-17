## Prepare the Index

First of all, after starting up our cluster, you can check your indices with 
the below request. This request will return you the indices of your cluster. 

```
# Get All Indices
GET _cat/indices

yellow open testing Rji2aXwdS1mmMuHJ7GcDQQ 5 1      3 0   6.3kb   6.3kb
yellow open .kibana BhjpOiQmThq5jvpq0ohuHA 1 1      2 0  27.3kb  27.3kb
```

### Create the Index

To create a new index, use `PUT` request like the following. You can also set 
some settings or you don't need. Both of them will work. Because, Elasticsearch
has some default settings and these default settings will use if you don't use
your customs. 

```
PUT gtd
{
    "settings" : {
        "number_of_shards" : 3,
        "number_of_replicas" : 2
    }
}
```

### Update Your Mapping

Mapping is like structure of your data. Yes, Elasticsearch is a NoSQL database.
Like every database, you can get more performance if you know your data. 
Following request will update your mapping. We expect that our data has a 
`latlon` field whose type is a `geo_point`, and a `date` field whose type 
is `date`.

```
# Update Mapping
PUT gtd/gtd/_mapping
{
  "properties": {
    "latlon": {
      "type": "geo_point"
    },
    "date": {
      "type": "date"
    }
  }
}
```