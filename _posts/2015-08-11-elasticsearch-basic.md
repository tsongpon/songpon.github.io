---
layout: post
title: Elasticsearch setup & basic use
comments: true
---

Elasticsearch is open source search engine written in Java. Elasticsearch is very powerful tool when you want to do full text search on big amount of data.

## Install Elasticsearch
- Download Elasticsearch from [here](https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.1.zip)
- Unzip to your preferred location
- Run `bin/elasticsearch`
- Go to `http://localhost:9200/` to Elasticsearch status, if everything OK you will get response like this

{% highlight %}
{
	status: 200,
	name: "Blackwing",
	cluster_name: "elasticsearch_tum",
	version: {
		number: "1.7.1",
		build_hash: "b88f43fc40b0bcd7f173a1f9ee2e97816de80b19",
		build_timestamp: "2015-07-29T09:54:16Z",
		build_snapshot: false,
		lucene_version: "4.10.4"
	},
	tagline: "You Know, for Search"
}
{% endhighlight %}
