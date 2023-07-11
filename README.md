
# RayVentory Catalog
###  The software catalog with added value
In RayVentory Catalog, inventoried raw data is assigned to applications using AI-powered software recognition and then presented in prepared reports.

![Screenshot](catalog.png)

## Getting Started
These instructions will cover usage information and for the docker container 

### Prerequisities
In order to run this container you'll need docker installed.

* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)

On Windows, make sure to use Linux Containers, WSL2 is recommended. 

### Usage
The default configuration consists of two containers:
* A database powered by mongoDB
* A container with frontend and backend for the catalog

The default configuration is standalone and should work out-of-the-box.

#### Installation with docker-compose
The easiest way to run the image with reasonable default is to use `docker-compose` command.

 1. Get the [`docker-compose.yml`](docker-compose.yml) file from this repository
 2. Login to Raynet container registry with credentials provided by Raynet
 3. In the folder containing the downloaded definition, run the following command: `docker-compose up -d`. 
 3. Login to [`http://localhost:8080`](http://localhost:8080) and use the following credentials:
- Login: `root`
- Password: `root`
 5. Provide the valid license for the product.
 6. After log-in, change your root password and create application users.

 ##### The image #####
RayVentory Catalog is available on docker hub:
[`https://hub.docker.com/r/raynetgmbh/rayventory-catalog`](https://hub.docker.com/r/raynetgmbh/rayventory-catalog)

You can use tags `12.5` (recommended) or `stable` to get the last 12.5 or the last stable version respectively.

#### Environment Variables
Catalog main web service:
* `BASEURL` - The base URL which will be used to access the app.
* `MongoConnectionString` - The connection string for mongo database (by default set to the mongoDB created by `docker-compose`)
* `MongoDatabaseName` - The name of the mongoDB database
* `MongoUserName` - The user name used when connecting to the mongoDB
* `MongoPassword` - The password used when connecting to the mongoDB
* `Logging__LogLevel__Default` - The default logging level

Database:
* `ServiceConfig__MongoConfiguration__UserName` - The user name for mongo database
* `ServiceConfig__MongoConfiguration__DatabaseName` - The database name for mongo database
* `ServiceConfig__MongoConfiguration__Password` - The password for mongo database

Massage queue:
* `MessageQueue__HostName` - The host name of the message queue
* `MessageQueue__QueuePrefix` - A string, used to prefix all queue objects
* `MessageQueue__User` - The user for message queue
* `MessageQueue__Password` - The password for message queue

File storage
* `FileStorage__HostName` - The host name of the min.io service
* `FileStorage__Bucket` - The name of the bucket
* `FileStorage__User` - The user name
* `FileStorage__Password` - The password
* `FileStorage__Port` - The port

* Worker-related
* `WorkerType` - Type of tasks that the given worker accepts (a single value or comma-separated list)

## Find Us

* [Raynet GmbH corporate website](https://raynet.de)
* [Raynet EALM GitHub](https://github.com/raynetEALM)
