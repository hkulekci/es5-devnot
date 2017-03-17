## Ingest Node

We can use logstash for manipulating out data while indexing our elastic 
cluster. With Elastic 5.x, we can also use *ingest node* to pre-process our
documents. 

Ingest node is enabled by default for all nodes. You can disable for some nodes,
and you can create your dedicated ingest node. Check the following 
configurations of `elasticsearch.yml`:

```
# dedicated ingest node configuration
node.data: false
node.master: false
node.ingest: true
```

### Pipeline

Pipelines are a series of processors that are executed to change your data or 
types. 

```
{
  "description" : "Your Pipeline Description",
  "processors" : [ ... ]
}
```

You can check pipelines that had already created on your systems with the below 
request.

```
# Get Ingest Pipelines
GET _ingest/pipeline
```

For our examples, we create a pipeline and we will update our `Location` and 
`Date` fields of our data. 

```
PUT _ingest/pipeline/my_pipeline
{
  "description" : "Crimes in Chicago Pipeline",
  "processors" : [
    {
      "script": {
        "lang": "painless",
        "inline": "ctx.Location = ctx.Location.substring(1,ctx.Location.length()).substring(0, ctx.Location.length()-1)"
      }
    },
    {
      "date" : {
        "field" : "Date",
        "target_field" : "Date",
        "formats" : ["MM/dd/yyyy HH:mm:ss a"],
        "timezone" : "UTC"
      }
    }
  ]
}
```

### Simulating Our Pipeline

We have created a pipeline for our Global Terrorism Dataset. Now, let's look 
our example to confirm it work correctly. In Elasticsearch, there is a simulate 
api interface. You should send your pipeline and documents like following 
example.

```
POST _ingest/pipeline/_simulate
{
    "pipeline": { ... },
    "docs": [
        {...},
        {...},
    ]
}
```

You can check the below example for simulating our example ingest pipeline.

```
POST _ingest/pipeline/_simulate
{
  "pipeline" : {
    "description" : "Crimes in Chicago Pipeline",
    "processors" : [
      {
        "script": {
          "lang": "painless",
          "inline": "ctx.Location = ctx.Latitude + ',' + ctx.Longitude"
        }
      },
      {
        "date" : {
          "field" : "Date",
          "target_field" : "Date",
          "formats" : ["MM/dd/yyyy HH:mm:ss a"],
          "timezone" : "UTC"
        }
      }
    ]
  },
  "docs" : [
    {
      "_index": "index",
      "_type": "type",
      "_id": "id",
      "_source":{"Date": "05/03/2016 10:00:00 PM", "Latitude":"41.893026751", "Longitude": "-87.626750829"}}
  ]
}
```