# ODH - Open Database Hunting
Where do most data breaches originate? From an open webserver somewhere, hosting an unauthenticated database. How do people find them? They use services like Censys, Shodan, and more. 

Here's how to find all types of databases through each service.

- **[Databases](#databases)**
  - [ElasticSearch](#elasticsearch)
      - [Exfiltration](#exfiltration)
      - [Ports](#ports) 
      - [Identifiers](#identifiers)
  - [Redis](#redis)
      - [Exfiltration](#exfiltration-1)
      - [Ports](#ports-1)
  - [Amazon S3](#amazons3)
      - [Exfiltration](#exfiltration-2)
      - [Ports](#ports-2)
      - [Identifiers](#identifiers-1)
  - ~~[MongoDB](#mongodb)~~
- **[Services](#services)**
  - [Censys.io](#censysio)
      - [Queries](#queries)
  - ~~[BinaryEdge](#binaryedge)~~
  - ~~[Shodan](#shodan)~~


# Databases
Here's all the different types of databases you can find using the services I have mentioned. Note, some of these will require authentication or 3rd party software to access. There is not a 100% success rate.
## ElasticSearch
ElasticSearch is a type of database, that does not have authentication by default. This is great for us, as most of these will be unsecured and easy to access.

### Exfiltration
There is a very nice Chrome extension, called ElasticVue. This application allows you to browse an ElasticSearch database without making raw requests. It provides a nice GUI that I find very informative. 
[https://elasticvue.com/](https://elasticvue.com/)

### Ports:
```
Default: 9200/9201
Alternative: Any port that serves HTTP content
```
### Identifiers:

**JSON Raw**: 
```
tagline: "You know, for search."
```

**HTTP Title**:
```
none
```

**Favicon**: 

![](icons/elasticsearch/favicon.ico "ElasticSearch Favicon")

## Redis
Redis is commonly used as a caching service, database, and data storage server. It's quite complicated and most times you will only find data for websites. However, usually you can edit files in the cache right from the start. So even if you don't find sensitive information, you can edit stored HTML or data used in the website and elevate to stored XSS.

### Exfiltration
You can use a few common CLIs, or my favourite program: Redis Desktop Manager.
This program is fantastic, as it simplifies the entirety of an extremely complicated application. It's open source, but you can also buy Microsoft Store versions to support the developers. You can find out more about it here:
[https://github.com/uglide/RedisDesktopManager](https://github.com/uglide/RedisDesktopManager)

### Ports:
```
Default: 6379
Alternative: unkn.
```
## Amazon S3
You've probably heard of Amazon S3. This service is mainly a static file hosting server, called buckets. However, many can store sensitive files. Sometimes, credentials are leaked that allow you to modify the contents of the bucket. 

### Exfiltration
There is a command line application that you can use called `aws-cli`. This allows you to run various functions on these servers, such as listing, uploading, and modifiying files. 
(https://aws.amazon.com/cli/)[https://aws.amazon.com/cli/]
### Ports:
```
Default: 80/443/8080
Alternative: Any port that serves HTTP content
```
### Identifiers:
**CNAME**:
```
[bucketname].s3.[region].amazonaws.com
```
**HTML Raw**:
```
<ListBucketResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
```
**HTTP Title**:
```
bucket_name/none
```
# Services
## Censys.io
Censys is a very similar service to Shodan, however it gives us a major benifit over Shodan. Censys does have a paid license, however it does not limit search results like Shodan does. Censys allows you to view every page of results, no matter what. You do only get 250 searches per month, though I think that it more than enough.
https://censys.io

### Queries
With Censys you have interesting options for querying and searching. They offer quite advanced search options, however in my experience they often give inaccurate results.

I am quite a fan of these search options:
```
443.https.tls.certificate.parsed.names:google.com
```
This option allows you to filter by results with SSL certificates mentioning the domain `google.com`. This allows you to filter IPs belonging to this organization. 
```
ports:9200 AND NOT 443.https.tls.certificate.parsed.names:*
```
This query allows you to filter for ElasticSearch instances, that do not have a domain tied to them. This allows you to find hidden VPSes or networks hosting databases. Though sometimes you will come across personal results.

## BinaryEdge
\[TODO\]
## Shodan
\[TODO\]
