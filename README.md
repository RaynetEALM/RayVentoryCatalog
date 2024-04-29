
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
The default configuration consists of the following containers:
* A database powered by MongoDB
* A message queue powered by RabbitMQ
* A file storage powered by min.io
* A container with frontend and backend for the catalog
* A set of one or more workers

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

You can use tags `12.6` (recommended) or `stable` to get the last 12.6 or the last stable version respectively.

#### Environment Variables

##### Catalog main web service #####
* `Logging__LogLevel__Default` - The default logging level
* `Synchronization__CachingJobCronExpression` - The cron expression that describe the schedule of caching task (use hyphen `-` to disable automatic startup of this task)
* `Synchronization__AutoSyncJobCronExpression` - The cron expression that describe the schedule of synchronization task (use hyphen `-` to disable automatic startup of this task)
* `Vulnerabilities__CachingJobCronExpression` - The cron expression that describe the schedule of vulnerabilities recache task (use hyphen `-` to disable automatic startup of this task)

#### Mongo database related settings ####
* `ServiceConfig__MongoConfiguration__ConnectionString` - The connection string for mongo database (by default set to the MongoDB created by `docker-compose`)
* `ServiceConfig__MongoConfiguration__DatabaseName` - The name of the MongoDB database
* `ServiceConfig__MongoConfiguration__AuthDatabaseName` - The name of the MongoDB authentication database
* `ServiceConfig__MongoConfiguration__UserName` - The user name used when connecting to the MongoDB
* `ServiceConfig__MongoConfiguration__Password` - The password used when connecting to the MongoDB
* `ServiceConfig__MongoConfiguration__UseTls` - Specifies whether to use TLS for secure communication with the MongoDB server.
* `ServiceConfig__MongoConfiguration__AllowInsecureTls` - Determines whether to allow connections over TLS with certificates that cannot be verified.
* `ServiceConfig__MongoConfiguration__CheckCertificateRevocation` - Indicates whether to check for certificate revocation status during TLS handshake.
* `ServiceConfig__MongoConfiguration__CertPemFilePath` - The file path to the SSL certificate and key. 
* `ServiceConfig__MongoConfiguration__CertCaFilePath` - The file path to the certificate authority (CA) file. 
* `ServiceConfig__MongoConfiguration__ReplicaSetName` - The name of the replica set in MongoDB.

Both the Web and Worker services support environment variables for configuring MongoDB. However, there's a slight difference in how you should prefix the MongoDB configuration variables for each module:
* For Web service `ServiceConfig__MongoConfiguration__` (for example: `ServiceConfig__MongoConfiguration__ConnectionString`)
* For Worker service `MongoConfiguration__` (for example: `MongoConfiguration__ConnectionString`)

Make sure that these value match with environment variables belonging to the database services, or that they are set-up to point to a service outside of the container set-up.

##### Message queue related settings #####
* `MessageQueue__HostName` - The host name of the message queue
* `MessageQueue__QueuePrefix` - A string, used to prefix all queue objects
* `MessageQueue__User` - The user for message queue
* `MessageQueue__Password` - The password for message queue
* `MessageQueue__Port` - The port for message queue

Make sure that these value match with environment variables belonging to the message queue services, or that they are set-up to point to a service outside of the container set-up.

##### File storage related settings #####
* `FileStorage__HostName` - The host name of the min.io service
* `FileStorage__Bucket` - The name of the bucket (must be between 3 and 63 characters long and can consist only of lowercase letters, numbers, dots `.`, and hyphens `-`)
* `FileStorage__User` - The user name
* `FileStorage__Password` - The password
* `FileStorage__Port` - The port

Make sure that these value match with environment variables belonging to the file storage services, or that they are set-up to point to a service outside of the container set-up.

##### Worker-related #####
* `WorkerType` - Type of tasks that the given worker accepts (a single value or comma-separated list)
* `Logging__LogLevel__Default` - The default logging level
  
## Find Us

* [Raynet GmbH corporate website](https://raynet.de)
* [Raynet EALM GitHub](https://github.com/raynetEALM)
* [RayVentory Catalog repository on Docker Hub](https://hub.docker.com/r/raynetgmbh/rayventory-catalog)
