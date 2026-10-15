# search-services
This repo includes a centralized configuration for services used by Search.gov applications, including:

- [search-gov](https://github.com/GSA/search-gov)
- [spider](https://github.com/GSA-TTS/searchgov-spider)

## Prerequisites
In order to run the services, you will need to install [Docker](https://www.docker.com/get-started).  We recommend setting the max memory alloted to Docker to 4GB (in Docker Desktop, Preferences > Resources > Advanced). See [the wiki](https://github.com/GSA/search-services/wiki/Docker-Command-Reference) for more documentation on basic Docker commands.

## Services
The docker-compose.yml file configures each service. You can refer to [Matrix](https://github.com/GSA/search-services#docker-services-matrix) on how to run required services for each application.

## Docker services matrix:
| Application/Repo | Command | Profile name | Services |
| --- | --- | --- | --- |
|  | `docker compose up` | N/A | MySQL, Redis, OpenSearch, OpenSearch Dashboards |
| search-gov |`docker compose --profile search-gov up` | search-gov | MySQL, Redis, OpenSearch, OpenSearch Dashboards, search-gov, resque-workers, resque-scheduler, spider, spider-scheduler, spider-sitemap |

Alternatively, you can run a subset of the services, i.e.:
```
docker compose up mysql opensearch redis
```

Each repo uses one or more of the following services:

### [MySQL](https://dev.mysql.com/doc/refman/8.0/en/)
Database backend required by search-gov.

### [Redis](https://redis.io/)
search-gov uses the Redis key-value store for caching, queue workflow via Resque, and some analytics. Optionally, you can install the [Redis CLI](https://redis.io/docs/manual/cli/).

### [OpenSearch](https://opensearch.org/)
OpenSearch is an open-source search and analytics suite used by search-gov. Locally, it runs on port [9300](http://localhost:9300/).

### [OpenSearch Dashboards](https://opensearch.org/docs/latest/dashboards/)
OpenSearch Dashboards is not required by the applications, but can be very useful for debugging OpenSearch. OpenSearch Dashboards are available at <http://localhost:5701>.
