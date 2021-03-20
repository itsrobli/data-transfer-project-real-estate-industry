# Data Transfer Project - Real Estate Industry (DTP-REI)

- [Data Transfer Project - Real Estate Industry (DTP-REI)](#data-transfer-project---real-estate-industry-dtp-rei)
  - [Overview](#overview)
  - [Current state](#current-state)
- [Background](#background)
  - [Background to the problem](#background-to-the-problem)
  - [Motivations and goals](#motivations-and-goals)
- [Architecture](#architecture)
  - [System components](#system-components)
    - [Data Models](#data-models)
    - [Adapters](#adapters)
      - [Data Adapters](#data-adapters)
      - [Authentication Adapters](#authentication-adapters)
    - [Task Management - the plumbing](#task-management---the-plumbing)
  - [System deployment](#system-deployment)

## Overview

The goal of this project is to make it really easy and quick to transfer data between participants in the real estate investment management industry.

I believe the solution is to establish industry standard protocols between data senders and receipients. Together, we will try to achieve this by building adapters and common data models in this project so that anybody can use them.

The framework and ideas of this Project are heavily borrowed from the original [Data Transfer Project](https://datatransferproject.dev). As suggested by the naming of this project, our approach is to extend these ideas and create the implementation as it applies to the real estate industry.

## Current state

This project is just starting. Please register your interest in the [discussion forum](https://github.com/itsrobli/data-transfer-project-real-estate-industry/discussions/2).

I am looking for people to contribute to the project. Together, we will continuing to define the architecture and implementation. Please participate in the [open issues](https://github.com/itsrobli/data-transfer-project-real-estate-industry/issues).

Any code in the repo is in active development, please do thorough testing and verification before implementing for production use.

# Background

##  Background to the problem

In the real estate industry, we frequently exchange a lot of information and data with each other because joint ownership of assets is very common. Every reporting period (usually monthly), real estate property, investment, and fund managers send each other tonnes of data so each can have a wholistic package of data to suit their own reporting and analytics needs.

Given everyone has their own systems and processes, there is work on both ends of the transporation of data:

- **Sender of data**: The Sender of the data must process it into the right data shape and reporting format for the receipient (it's common a PDF management report and some Excel tables is provided). This deliverable is often different to the way the sender reports the same information internally. In addition, each receipient will specify their own requirements which are often different from other receipients - this compounds the amount of work for the Sender. 

- **Receipient**: The receipient of this data often must translate the information into what their home systems will understand because this data will feed into various other reporting and analytics requirements.

Typically every month, these processes are done manually by an army of finance people across the industry who spend days and weeks translating each other’s spreadsheets into their home system.

## Motivations and goals

The motivation is to stop the suffering caused by this manual translation of data back and forth. This can be achieved by making sure the sender and the receipient are aligned by defininig a common sharing protocol.

Given it's a common problem with limited specialist resources to solve it, and requires widespread adoption, running it as an open source project is the best way to concentrate the effort and ensure everyone can benefit and use it.

# Architecture

The system's main goal is to make it easy for a new participant to adopt the standards and get immediate benefit. Principles to follow to enable this:

- Use existing standards where possible - for example, don't re-invent REST or OAuth.

- The majority of work for a new Participant should be on the Adapters that enable import and export functionality. They should not have to modify their existing APIs, authorisation systems, and other internal core systems.

- DTP-REI infrastructure deployment should be standard (i.e. Docker).

## System components

1. **Data Models​** are the canonical formats that establish a common understanding of how to
transfer data.

2. **Adapters​** provide a method for converting each Participant's proprietary data and
authentication formats into a form that is usable by the system (and therefore other Participants).

3. **Task Management Library**​ provides the plumbing to power the system.

![DTP-REI high level architecture](/documentation/dtp-rei-architecture-components.png)

### Data Models

The Data Model for transferring data assets consists of two parts: a file type and the additional metadata needed by the receiving Participant to accurately import the data. For example with financial data, the file type might be a standard format such as CSV, and the metadata would include information such as general ledger account code, description, period, amount, etc.

Data Models are clustered together, typically by industry grouping, to form Verticals. A Participant could have data in one or more Verticals. Verticals could be financials, tenants, properties, etc. Each Vertical has its own set of Data Models that enable seamless transfer of the relevant file types. For example, the Financials Vertical could have Data Models for cashflows, forecasts, budgets, and valuations.

Ideally, a Vertical will have a small number of well-defined and widely-adopted Data Models. In such a situation, the generally accepted standard will be used as the Data Model for that Vertical across real estate management companies and funds. This is not currently the case for most Verticals because Data Models have emerged organically in a largely disconnected ecosystem.

One goal of the DTP-REI is to encourage organisations to use common Data Models in their systems, which will happen if organisations take importing and exporting data into consideration when initially designing their systems or providing updates. Using a common Data Model will significantly reduce the need for companies to maintain and update proprietary APIs.

In the case where there is no standard Data Model for a Vertical, companies will want to collaborate and agree upon standardised Data Models, either during the DTP-REI development or in collaboration with external standards bodies. Without collaboration, each provider could have their own Data Model, and would have to create Adapters that would have to support the same number of Data Models as there are companies in the Vertical, which would reduce the usefulness of the DTP-REI.

Even where standard Data Models do exist, collaboration will be an ongoing and mutually beneficial shared commitment as APIs will need to be maintained to handle new features, evolving standards, or innovative new formats.

### Adapters

There are two main kinds of Adapters: Data Adapters and Authentication Adapters. These Adapters exist outside of a Participant's core systems and can be written either by the Participant itself, or by third parties that would like to enable data transfer to and from a Participant.

#### Data Adapters

Data Adapters are pieces of code that translate a given Participant’s APIs into Data Models used by the DTP-REI. Data Adapters come in pairs: an exporter that translates from the Participant's API into the Data Model, and an importer that translates from the Data Model into the Participant's API.

#### Authentication Adapters

Authentication Adapters are pieces of code that allow users (likely employees of the organisations) to authenticate their accounts before transferring data out of or into another Participant's systems. OAuth is likely to be the choice for most Participants, however the DTP-REI is agnostic to the type of authentication.

Note: Under this system, emailing spreadsheets could be seen as a type of transport and authentication.


### Task Management - the plumbing

The Task Management Libraries handle background tasks, such as calls between the two relevant Adapters, secure data storage, retry logic, rate limiting, pagination management, failure handling, and individual notifications.

The DTP-REI aims to develope a collection of Task Management Libraries as a reference implementation for how to utilise the Adapters to transfer data between two Participants. If preferred, Participants can choose to write their own implementation of the Task Management Libraries that utilise the Data Models and Adapters of the DTP-REI.

## System deployment

The method of deployment will determine how the system's components work together. As with the original DTP, multiple deployment models should work. However, for now, we will focus on the distributed model.

This model requires at least one Participant to spin-up their own Host Platform using the relevent components of this project. 

As can be seen below, Participant C and E cannot directly transfer data to each other because neither has a Host Platform.

![DTP-REI high level system deployment](/documentation/dtp-rei-architecture-system-deployment.png)
