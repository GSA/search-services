# search-services
This repo includes a centralized configuration for services used by Search.gov applications, including:

- [search-gov](https://github.com/GSA/search-gov)
- [i14y](https://github.com/GSA/i14y)
- [ASIS](https://github.com/GSA/asis)

## Prerequisites
In order to run the services, you will need to install [Docker](https://www.docker.com/get-started).  We recommend setting the max memory alloted to Docker to 4GB (in Docker Desktop, Preferences > Resources > Advanced). See [the wiki](https://github.com/GSA/search-services/wiki/Docker-Command-Reference) for more documentation on basic Docker commands.

## Services
The docker-compose.yml file configures each service. You can run all the services with a single command:
```
docker compose up
```
Alternatively, you can run a subset of the services, i.e.:
```
docker compose up mysql elasticsearch7\
```

Each repo uses one or more of the following services:

### [MySQL](https://dev.mysql.com/doc/refman/5.7/en/)
Database backend required by search-gov.

### [Elasticsearch](https://www.elastic.co/elasticsearch/)
Services for Elasticsearch 7 are provided here.

Elasticsearch plugins:
* [analysis-kuromoji](https://www.elastic.co/guide/en/elasticsearch/plugins/current/analysis-kuromoji.html)
* [analysis-icu](https://www.elastic.co/guide/en/elasticsearch/plugins/master/analysis-icu-analyzer.html)
* [analysis-smartcn](https://www.elastic.co/guide/en/elasticsearch/plugins/current/analysis-smartcn.html)

Some specs depend upon Elasticsearch having a valid trial license. A 30-day trial license is automatically applied when the cluster is initially created. If your license expires, you can rebuild the cluster by [rebuilding the container and its data volume](https://github.com/GSA/search-gov/wiki/Docker-Command-Reference/_edit#recreate-an-elasticsearch-cluster-useful-for-restarting-a-trial-license). 

#### Elasticsearch 7
All of our applications use Elasticsearch 7 in production for full-text search. Locally, it runs on the default port [9200](http://localhost:9200/).

### [Redis](https://redis.io/)
search-gov and ASIS use the Redis key-value store for caching, queue workflow via Resque (search-gov) and Sidekiq (ASIS), and some analytics. Optionally, you can install the [Redis CLI](https://redis.io/docs/manual/cli/).

### [Tika](https://tika.apache.org/)
Used by search-gov for extracting plain text from PDFs, etc. The [Tika REST server](https://cwiki.apache.org/confluence/display/TIKA/TikaServer) runs on port [9998](http://localhost:9998).

### [Kibana](https://www.elastic.co/kibana)
Kibana is not required by the applications, but can be very useful for debugging Elasticsearch. Confirm Kibana is available for the Elasticsearch 6 cluster by visiting <http://localhost:5601>. Kibana for the Elasticsearch 7 cluster should be available at <http://localhost:5607>.
