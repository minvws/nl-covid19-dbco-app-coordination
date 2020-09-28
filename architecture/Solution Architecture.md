# COVID-19 DBCO App - Solution Architecture


**Version:** 0.1 

# Introduction

The Dutch Ministry of Health, Welfare and Sport is developing an app to aid the GGD in their contact tracing (Dutch: Bron & Contact Onderzoek, BCO) efforts. The name of the app has yet to be determined, for now we use the working title 'DBCO App' (Digitale ondersteuning Bron & Contact Onderzoek App). This document describes the functional and technical architecture of the DBCO app.

# Table of contents

- [COVID-19 DBCO App - Solution Architecture](#covid-19-dbco-app---solution-architecture)
- [Introduction](#introduction)
- [Table of contents](#table-of-contents)
- [Requirements](#requirements)
  * [GGD Requirements](#ggd-requirements)
  * [General Guiding principles](#guiding-principles)
- [Key characteristics](#key-characteristics)
- [High Level Architecture](#high-level-architecture)
- [Flows](#flows)
  * [Onboarding](#onboarding)
  * [Case Creation](#case-creation)
  * [Collecting data](#collecting-data)
  * [Submitting data to the backend](#submiting-data-to-the-backend)
  * [Making data available to GGD](#making-data-available-to-GGD)
- [System Landscape](#system-landscape)
- [Security & Privacy](#security--privacy)
  * [Overview](#overview)
  * [Attack Surface Minimisation](#attack-surface-minimisation)
  * [Data cleanup](#data-cleanup)
- [Backend Considerations](#backend-considerations)
  * [Backend overview](#backend-overview)
  * [Infrastructure](#infrastructure)
  * [App/Device Verification](#appdevice-verification)
- [App Considerations](#app-considerations)
  * [Native vs hybrid development](#native-vs-hybrid-development)
  * [Lifecycle Management](#lifecycle-management)

# Requirements

## GGD requirements

The app is build around a set of GGD requirements. For the first ('MVP') version of the app the requirements are taken from:

* Bijlage 1 - Functionaliteit MVP en Oktober MVP (PVE Oktober MVP bijlagen.docx) 

## General Guiding principles

In addition to the requirements, we have defined a number of guiding principles that a solution must adhere to. This means that this project has a number of key contextual requirements that drive or otherwise define the architecture or are used as a benchmark:

* [Baseline Informatiebeveiliging Overheid 1.04](https://bio-overheid.nl/media/1400/70463-rapport-bio-versie-104_digi.pdf)

* [Algemene Verordening Gegevensbescherming (AVG)](https://autoriteitpersoonsgegevens.nl/sites/default/files/atoms/files/verordening_2016_-_679_definitief.pdf) 

* [Handreiking Mobiele App Ontwikkeling en Beheer 3.0](https://www.noraonline.nl/images/noraonline/a/a5/Handreiking_Mobiele_App_3.0.pdf) 

* [Web Content Accessibility Guidelines 2.1](https://www.w3.org/TR/WCAG21/)

* [NCSC beveiligingsrichtlijnen voor webapplicaties](https://www.ncsc.nl/documenten/publicaties/2019/mei/01/ict-beveiligingsrichtlijnen-voor-webapplicaties)

* [NCSC beveiligingsrichtlijnen voor mobiele apps](https://www.ncsc.nl/documenten/publicaties/2019/mei/01/ict-beveiligingsrichtlijnen-voor-mobiele-apps)

# Key characteristics

## Privacy by design

For the app we follow a Privacy by Design approach. This means:

* We will not collect more data than necessary. 
* Data that we do collect is protected with appropriate measures
* We apply end-to-end security

## Open Source

All source code will be made available on the ministry's GitHub account.

# High Level Architecture

The following diagram shows a high level concept of the solution.

![High Level Architecture](images/HLA.png)

Todo: describe 'data sluis'.

Todo: describe concept of 'contact tasks' that the user gets to collect contact information.

# Flows

This chapter describes the core flow that we are following, which is derived from the requirement, UX research and various discussions with the health authority.

## Onboarding

Todo

## Data preparation

A user that installs the app before getting a positive test result can start to use the app to prepare for the BCO investigation. Because there's no specific case, this part of the flow is 'generic', in the sense that all users will get the same set of basic questions. Questions can, for example, be to list the people in your household.

The following diagram depicts the steps for this flow:

![Preparation](images/step1_preparation.png)

It is important that in this flow there is only generic interaction with the backend: to retrieve an app configuration and the list of initial tasks. The answers to the initial tasks stay local on the device and may help speed up the BCO conversation. 

## Pairing the device case with the BCO case

Once there is a BCO conversation the user is asked if the app is already installed or if not, to install it. The user gets handed a code to be able to link the contents in the app to the user's BCO case. Note: for the CoronaMelder app it was chosen to have the user read a code to the operator. In this case we chose the other way round, because the user might not have the app installed just yet, and may need to write down the code and install and pair the app after the call.

The following diagram depicts the pairing process:

![Pairing](images/step2_pairing.png)

## Collecting data

During the BCO conversation, additional tasks will have been defined by the BCO expert. They might have talked about that goalkeeper in the football team that you accidentally hugged after a score, so they might ask you to collect the data for that goalkeeper. These tasks are created using the GGD's BCO portal and the app retrieves them during/after the call.

The following diagram depicts the process of retrieving these tasks and presenting them to the user.

![Data collection](images/step3_datacollection.png)

## Submitting data to the backend

When the user has completed the tasks by filling out the contact details, the user will upload them to the backend. The following diagram depicts the upload process:

![Data upload](images/step4_dataupload.png)

## Making data available to GGD

Todo

# System Landscape

Todo

# Security & Privacy

## Overview

The details surrounding the security and privacy implementation of the app is laid out in the document [‘Crypto Architecture’](Crypto Architecture.md). While the details and rationale surrounding the choices can be found in that document, for this solution architecture we have outlined the key principles from the preliminary version in the following diagram.

Todo

Each part of the diagram tries to address a number of key aspects:

* Source authenticity: how can we ensure that data comes from a known / trusted source

* Destination authenticity: how can we ensure that data gets sent to a known / trusted source

* Data integrity: how can we ensure that the data has not been tampered with.

* Data protection: how can we ensure that only authorized people can access the data

## Attack Surface Minimisation

We practice 'attack surface minimisation' to reduce risks. This means we pay attention to the following:

* No more API calls than necessary for the operation of the app (no exposure of generic REST endpoints)
* No more fields in input/output than necessary (calls will provide specific answers instead of generic entities)
* Internal / machine to machine API calls separated from public / app to backend API calls
* Where possible, deliver data via push between APIs instead of via pull.

## Data cleanup

We don't want to keep data around longer than necessary. Therefor we have defined a few rules we apply for data cleanup:

### Backend 

Todo

### Apps

Todo



# Backend Considerations 

## Backend overview

Todo

## App/Device Verification

This part is taken directy from the CoronaMelder architecture, and we follow the route we have taken there:

The Google Reference Implementation of a backend for exposure notification suggests the use of DeviceCheck (iOS) and Safetynet Attestation (Android) to validate if a request comes from a genuine android device and/or from the official app:

* [https://github.com/google/exposure-notifications-server/blob/master/docs/server_functional_requirements.md](https://github.com/google/exposure-notifications-server/blob/master/docs/server_functional_requirements.md)

The documentation for DeviceCheck and Safetynet Attestation can be found here:

* [https://developer.apple.com/documentation/devicecheck](https://developer.apple.com/documentation/devicecheck)

* [https://developer.android.com/training/safetynet/attestation](https://developer.android.com/training/safetynet/attestation)

We have decided not to apply these platform specific checks. First, it relies on a server API at Apple and Google, which can be down and could be a privacy risk.

Second, the Android Developer blog states: 

"*In other words, not all users who fail attestation are necessarily abusers, and not all abusers will necessarily fail attestation. By blocking users solely on their attestation results, you might be missing abusive users that don't fail attestations. Furthermore, you might also be blocking legitimate, loyal customers who fail attestations for reasons other than abuse*" (NOTE:  https://android-developers.googleblog.com/2017/11/10-things-you-might-be-doing-wrong-when.html)

The safetynet attestation documentation further states about attestation failure: *"Most likely, the device launched with an Android version less than 7.0 and it does not support hardware attestation. In this case, Android has a software implementation of attestation which produces the same sort of attestation certificate, but signed with a key hardcoded in Android source code. Because this signing key is not a secret, the attestation could have been created by an attacker pretending to provide secure hardware"* (NOTE:  https://developer.android.com/training/articles/security-key-attestation)

This leads us to believe that when applying these checks, we introduce risks and dependencies while not gaining a substantial amount of security.

# App Considerations

## Native vs hybrid development

Mobile apps will be implemented as native applications, with Swift as the language used for iOS development and Kotlin for Android development.

We have carefully considered whether to do native development or use a cross platform technology, and the following arguments were leading:

* There are no requirements or constraints that dictate the use of cross platform tools.

* The available development team has sufficient capability in native app development.

* It is expected that, should we need help from Google or Apple to resolve issues while implementing this app, they can do so more efficiently if we use the development stack provided by the vendors.

* In order to ease [security] code-reviews and thus keeping them accessible to a wider audience, it is prudent to keep the app's stack and usage of programming paradigms as vanilla and lean as possible.

## Lifecycle Management

Apps run on the user’s device and updates require a review process that is not entirely under our control. To mitigate these factors that are outside our control, apps should implement a form of lifecycle management. This includes the following features:

* Configuration values or content that are expected to change should be retrieved from a server.

* Apps should offer a ‘forced upgrade’ (i.e. if a new version is available that fixes a critical bug, it should be possible to force the user to upgrade). 

