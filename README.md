# Overview

The goal of this project is to make it really easy and quick to transfer data between participants in the real estate investment management industry.

We believe the solution is to establish industry standard protocols between data senders and receipients. We will try to achieve this by building adapters and standard data models in this project so that anybody can use them.

The framework and ideas of this Project are heavily borrowed from the original [Data Transfer Project](https://datatransferproject.dev). As suggested by the naming of this project, our approach is to extend these ideas and create the implementation as it applies to the real estate industry.

# Current state

This project is just starting. Please register your interest in the [discussion forum](https://github.com/itsrobli/data-transfer-project-real-estate-industry/discussions/2).

We are actively looking for people to contribute to the project. We are continuing to define the architecture and implementation. Please participate in the [open issues](https://github.com/itsrobli/data-transfer-project-real-estate-industry/issues).

Any code in the repo is in active development, please do thorough testing and verification before implementing for production use.

# Background and motivations

##  Background to the problem

In the real estate industry, we frequently exchange a lot of information and data with each other because joint ownership of assets is very common. Every reporting period (usually monthly), real estate property, investment, and fund managers send each other tonnes of data so each can have a wholistic package of data to suit their own reporting and analytics needs.

Given everyone has their own systems and processes, there is work on both ends of the transporation of data:

- **Sender of data**: The Sender of the data must process it into the right data shape and reporting format for the receipient (it's common a PDF management report and some Excel tables is provided). This deliverable is often different to the way the sender reports the same information internally. In addition, each receipient will specify their own requirements which are often different from other receipients - this compounds the amount of work for the Sender. 

- **Receipient**: The receipient of this data often must translate the information into what their home systems will understand because this data will feed into various other reporting and analytics requirements.

Typically every month, these processes are done manually by an army of finance people across the industry who spend days and weeks translating each other’s spreadsheets into their home system.

## Motivations and goals

The motivation is to stop the suffering caused by this manual translation of data back and forth. This can be achieved by making sure the sender and the receipient are aligned by defininig a common sharing protocol.

Given it's a common problem with limited specialist resources to solve it, and requires widespread adoption, running it as an open source project is the best way to concentrate the effort and ensure everyone can benefit and use it.

# High-level architecture



