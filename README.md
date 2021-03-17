# ODH - Open Database Hunting
Where do most data breaches originate? From an open webserver somewhere, hosting an unauthenticated database. How do people find them? They use services like Censys, Shodan, and more. 

Here's how to find all types of databases through each service.

- **[Services](#services)**
  - [Censys.io](#censysio)
  - [BinaryEdge](#binaryedge)
  - [Shodan](#shodan)
- **[Databases](#databases)**
  - [ElasticSearch](#elasticsearch)
      - [Exfiltration](#exfiltration)
      - [Ports](#ports) 
      - [Web Identifiers](#webidentifiers)
  - [Redis](#redis)
      - [Exfiltration](#exfiltration-1)
      - [Ports](#ports-1)
  - [MongoDB](#mongodb)

# Services
## Censys.io
Censys is a very similar service to Shodan, however it gives us a major benifit over Shodan. Censys does have a paid license, however it does not limit search results like Shodan does. Censys allows you to view every page of results, no matter what. You do only get 250 searches per month, though I think that it more than enough.
https://censys.io
## BinaryEdge
## Shodan
# Databases
Now that you know how to use the mentioned services to find these databases, here's what you need for each type. 
## ElasticSearch
ElasticSearch is a type of database, that does not have authentication by default. This is great for us, as most of these will be unsecured and easy to access.

### Exfiltration
There is a very nice Chrome extension, called ElasticVue. This application allows you to browse an ElasticSearch database without making raw requests. It provides a nice GUI that I find very informative. 
[https://elasticvue.com/](https://elasticvue.com/)

### Ports:
```
Default: 9200/9201
Alternative: 80/443/8080 (default HTTP ports)
```
### Web Identifiers:

**HTML RAW**: 
```
tagline: "You know, for search."
```

HTML Title:
```
none
```

ICON: 

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
