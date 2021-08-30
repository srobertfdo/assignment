# Assignment

This Assignment contains Microservices to securely store data in a file format and allow the user to read and update when required. 

# Table of contents
* Introduction
* Overview
* Requirements
* Installation & Setup
* Test & Execute Application


## Introduction

This Assignment has Microservices to securely store data in a file format and allow the user to read and update when required.  Fiel format can be both CSV and XML file format. Each is independently built & deployable.

## Overview

  The assignment has 2 microservices and it uses a message broker and REST APIs for communication. All data transfer happens in a secure way using encryption and protocol buffer format. Also, the application provides secure storage containers to store files. Below is our application architecture.  


![Alt text](/assignment.png?raw=true "Assigment | Diagram")

### Services

Microservices are developed in Node JS using [ AdonisJs](https://legacy.adonisjs.com/docs/4.1/about). AdonisJs is a Node.js MVC framework that runs on all major operating systems. It offers a stable ecosystem to write server-side web applications so you can focus on business needs over finalizing which package to choose or not.

AdonisJs favors developer joy with a consistent and expressive API to build full-stack web applications or micro API servers.

Following packages from AdonisJs are used to make service more effective. 
- [Service providers](https://legacy.adonisjs.com/docs/4.1/service-providers)
- [Vaidator](https://legacy.adonisjs.com/docs/4.1/validator)
- [ORM](https://legacy.adonisjs.com/docs/4.1/lucid)
- [Exception handling](https://legacy.adonisjs.com/docs/4.1/exceptions)
- [Logs](https://legacy.adonisjs.com/docs/4.1/logger)
- [Unit & Functionality Test](https://legacy.adonisjs.com/docs/4.1/testing)
- [Encryption](https://legacy.adonisjs.com/docs/4.1/encryption-and-hashing)

### Message broker

[Rabbit MQ](https://www.rabbitmq.com/) user for communication between services. It is one of the most popular message brokers that run on top of Advanced Message Queuing Protocol (AMQP). There are four main components forming AMQP protocol: Publisher, Exchange, Queue, Consumer. 

Our application uses the Exchange method Direct for communication. We can also configure it in our applications. I have used [amqplib]() npm package to implement Rabbit MQ. Here Service one will be Publisher and Service two will be a consumer. 

![Alt text](/mq.jpeg?raw=true "Rabbit MQ | Diagram")

### Protocol buffer

Here I have used [Google protocol buffer](https://developers.google.com/protocol-buffers) to encode the messages between services. I have achieved this in Node Js using [protobufjs](https://www.npmjs.com/package/protobufjs)

### Blob Storage 

[Azure blob storage](https://azure.microsoft.com/en-in/services/storage/blobs/) has been used to store user files in the cloud. We can configure the storage and container details in Env. [azure/storage-blob](https://www.npmjs.com/package/@azure/storage-blob) is used for this.  

### Database

[Postgres sql](https://www.postgresql.org/) database is used for storing user file blob information. 

### REST API
Rest API is used for only reading data from service two. That API call is also encrypted using aes-256-cbc Algorithm. Secret keys are stored in Env for decryption.

## Requirements

1. NodeJS
2. Docker
3. Azure Blob Storage Connection String
4. Below Repositories 

- https://github.com/srobertfdo/assignment
- https://github.com/srobertfdo/assignment_service_one
- https://github.com/srobertfdo/assignment_service_two

# Installation & Setup

1. First install Nodejs for Microservices. [Refer](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) 

2. Second install Docker to run RabitMq and Postgres SQL. [Refer](https://docs.docker.com/engine/install/)
 
3. Create Azure blob storage. [Refer](https://docs.micr
osoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal)
4. Run Rabbit Mq and Postgres SQL docker composer. Please make sure docker is up and running.

```bash

git clone https://github.com/srobertfdo/assignment

cd assignment

docker compose -f docker-compose.yml up

```

5. Run service one

```bash

git clone https://github.com/srobertfdo/assignment_service_one

cd assignment_service_one

npm i --save

cp .env.example .env

npm start

```

Now you can see below:

```
> adonis-api-app@4.1.0 start
> node server.js

info: serving app on http://127.0.0.1:3333
```

6. Run service two

```bash

git clone https://github.com/srobertfdo/assignment_service_one

cd assignment_service_one

npm i --save

cp .env.example .env

```

Update below env variables with Azure credentials and container name.

```
BLOBE_STORAGE_CONNECTTION_STRING
BLOBE_STORAGE_CONTAINER
```

The start service

```bash

npm start

```

Now you can see below:

```
> adonis-fullstack-app@4.1.0 start
> node server.js

info: Consumer starts...!
info: serving app on http://127.0.0.1:3334
```

## Test & Execute Application

- Running test cases. (both service same comment)

```
npm test
```
Note: To pass all integration tests in Service one please make sure Service two is running. Because it verifies the data from service two. 

- Test APIs: Once everything is up and running use the below URL to swagger the document.

```
http://127.0.0.1:3333/docs
````
Here we go! Now we can test everything using a swagger. :)

Many Thanks!
