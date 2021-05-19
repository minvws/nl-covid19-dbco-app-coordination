#  GGD Contact - Portal

**Version:** 0.1 (Work in Progress)

## Introduction

The Dutch Ministry of Health, Welfare and Sport is developing an app (GGD Contact) and portal to aid the GGD in their contact tracing (Dutch: Bron & Contact Onderzoek, BCO) efforts. This document describes the functional and technical architecture of the **Portal** for caregivers.

Before you read this document, make sure you have read [this document](../Solution Architecture GGD Contact.md) first.

This document is a work in progress and will be adjusted during the project.

## Setup

The Portal is written in PHP (>= 7.4) and TypeScript. It uses the [Laravel](https://laravel.com) PHP framework to expose a front-end API to a VueJS application. 

The Portal uses MySQL as relational database to store its data. 

## Security
Private data is encrypted before being stored in the database. See [Security Design Overwegingen GGD Contact](../Security Design Overwegingen GGD Contact.md). 

The Portal is only reachable from a private network. Users are authenticated against an external system using OAuth.

## Concepts

### Service and Repository pattern

The Laravel based PHP frontend API uses the Service and Repository pattern to split the data layer and business logic. Controllers communicate with services that contain the business logic and access data through one or more repositories. Repositories contain the logic to retrieve and store data from/to a data store (e.g. MySQL or Redis). In most cases a repository is responsible for the data access for one model. Although sometimes a repository is also responsible for the data access to child models that the main model owns. 

These service and repository allow for easier unit testing as you can, for example, easily mock a repository and still test the business logic. 

### Fragments

The system needs to store answers to many different questions for each case. These questions will also change during the course of time. To keep the system flexible the "fragments" concept was introduced. Fragments are basically a storage mechanism for a group of questions and are represented in PHP as simple model classes. 

When the data is stored in the database the model classes are encoded to JSON, encrypted and stored in a table column. On retrieval the data is decrypted and decoded back to the PHP object structure. 

The same mechanism for encoding/decoding is used for data that is being sent from/to the frontend.

Fragment data is versioned. The version information is stored together with the fragment data and can be used to load the proper model class when retrieved from the database. Because all answers for a fragment are stored in a single column it is easy to support different versions of fragments being used by different cases. Storing an answer to a new question can be done by simply adding a field to a fragment class and adding some validation rules. No schema changes are necessary.

