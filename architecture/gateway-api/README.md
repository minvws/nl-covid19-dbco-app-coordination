#  GGD Contact - Gateway API

**Version:** 0.1 (Work in Progress)

## Introduction

The Dutch Ministry of Health, Welfare and Sport is developing an app (GGD Contact) and portal to aid the GGD in their contact tracing (Dutch: Bron & Contact Onderzoek, BCO) efforts. This document describes the functional and technical architecture of the **Gateway API** for the DBCO app.

Before you read this document, make sure you have read [this document](../Solution Architecture GGD Contact.md) first.

This document is a work in progress and will be adjusted during the project.

## Setup

The Gateway api is written in PHP (>= 7.4). It uses the [Laravel](https://laravel.com) PHP framework to expose a API to a external applications like Osiris(RIVM) and CoronaIT(GGD).

The Gateway api uses the databases MySQL and Redis to retrieve data.

## Security

The gateway-api is reachable using JWT authentication.

## API specs

The definition of the Gateway API can be found in [this Swagger File](gateway-api.yaml).

## External connections

### Osiris

The API exports formatted cases to the RIVM(not released yet).

### CoronaIT

The API to CoronaIT retrieves and sends case to the GGD(not released yet).