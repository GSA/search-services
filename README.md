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
docker compose up mysql elasticsearch7
```

Each repo uses one or more of the following services:

### [MySQL](https://dev.mysql.com/doc/refman/5.7/en/)
Database backend required by search-gov.

### [Elasticsearch](https://www.elastic.co/elasticsearch/)
Services for Elasticsearch 6 and 7 are both provided here.

#### Elasticsearch 6
All of our applications use Elasticsearch 6 in production for full-text search. Locally, it runs on the default port [9200](http://localhost:9200/).

**Please note: Elasticsearch 6 is not supported on M1 Macs.** Until all our repos use Elasticsearch 7 in mid-2022, Developers on M1s can run the remaining services with:
```
docker compose up mysql elasticsearch7 redis tika kibana7
```
You may also need to update the Elasticsearch host in each repo's `config/secrets.yml` or `config/elasticsearch.yml` file to specify `localhost:9207` to point to Elasticsearch 7.

#### Elasticsearch 7
Currently only used in development, running on port [9207](http://localhost:9207/).

### [Redis](https://redis.io/)
search-gov and ASIS use the Redis key-value store for caching, queue workflow via Resque (search-gov) and Sidekiq (ASIS), and some analytics. Optionally, you can install the [Redis CLI](https://redis.io/docs/manual/cli/).

### [Tika](https://tika.apache.org/)
Used by search-gov for extracting plain text from PDFs, etc. The [Tika REST server](https://cwiki.apache.org/confluence/display/TIKA/TikaServer) runs on port [9998](http://localhost:9998).

### [Kibana](https://www.elastic.co/kibana)
Kibana is not required by the applications, but can be very useful for debugging Elasticsearch. Confirm Kibana is available for the Elasticsearch 6 cluster by visiting <http://localhost:5601>. Kibana for the Elasticsearch 7 cluster should be available at <http://localhost:5607>.