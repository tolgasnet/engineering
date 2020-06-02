Last updated 1st June 2020

Version 0.1.0 

## Table of Contents <!-- omit in toc -->

- [1. Practices](#1-practices)
  - [XP](#xp)
  - [Agile](#agile)
  - [Lean](#lean)
  - [DDD](#ddd)
- [2. Architecture](#2-architecture)
  - [Characteristics](#characteristics)
  - [Service patterns](#service-patterns)
  - [Communication](#communication)
  - [Database](#database)
  - [Serverless](#serverless)
- [3. Development](#3-development)
  - [React](#react)
  - [Node.js](#nodejs)
    - [Javascript](#javascript)
    - [Error handling / logging](#error-handling--logging)
    - [Config](#config)
    - [Repos and branching](#repos-and-branching)
  - [Terminal](#terminal)
- [4. DevSecOps](#4-devsecops)
  - [Infrastructure as code](#infrastructure-as-code)
  - [Pipeline as code](#pipeline-as-code)
  - [Deployments](#deployments)
  - [DORA metrics](#dora-metrics)
- [5. Testing](#5-testing)
  - [End to end testing](#end-to-end-testing)
  - [Component testing](#component-testing)
  - [Unit testing](#unit-testing)

# 1. Practices

## XP

## Agile

## Lean

## DDD

# 2. Architecture

## Characteristics

## Service patterns

## Communication

## Database

## Serverless

# 3. Development

## React

## Node.js

### Javascript
* Use arrow functions.
* Use async/await.
* Use === operator.
* Use camel case for variables, constants, functions and pascal case for classes.
* Use ESlint with appropriate plugins.
* Use only the built-in Error object or extend it. Don't extend it multiple times.
* Handle/translate exceptions in wrappers for third party libraries, API's or databases.
* Use top level error handlers to decide the appropriate action. Use lover level error handlers to add the additional context. Always use error libraries to standardize the error context.

### Error handling / logging
* Document API error responses.
* Fail fast and gracefully. Use graceful degradation for API responses. If a non-critical piece of data could not be retrieved, return fail the whole response unnecessarily. However, if you know the request should fail, don't defer the responsibility to another object by returning null or an error object. Throw/Fail immediately. 
* Use either 500 or 200 for error responses. Advantage of using 500 is the api consumer can there is an error by checking status only. The advantage of using 200 for errors is you can then use 500s for other types of errors which are separate from business logic errors. There are examples of either usage patterns in big tech companies.
* Never use *console.log* so you can query through logs, separate by log levels, add json objects, etc.
* Log level *error* only for real critical errors ie. someone needs to look at it immediately.
* Use *unhandledRejection* event to be able to catch unhandled promise rejections.
* Use circuit breakers to avoid cascading errors.
  
### Config
* Separate config files into multiple sections or even files. This can make it easier to tell which values are used for which components.
* Separate the config values which have default values if the environment value is not there, and which values that should always be there and throw at start-up otherwise.

### Repos and branching
* Use either monorepos or polyrepos depending on use case. Monorepos have good advantages such as simpler maintenance, less switching between projects, PRs with better context, and easier code re-use.
* Use short-lived branches or trunk based development. Short lived branches enable frequent releases, conflict free merges and easy to review PRs. Trunk based development takes that a bit further and allows full continuous integration to main branch, every few minutes to a couple of hours. Trunk based development will require adopting feature toggles.
* Feature toggles should ideally be as close as to the top layer as possible, ie. web frontend, mobile client, or API interface. This will make sure the code branch is completely separate and different logical branches in the code doesn't get too complex with too many conditionals.

## Terminal

# 4. DevSecOps

## Infrastructure as code

## Pipeline as code

## Deployments

## DORA metrics

# 5. Testing

## End to end testing

## Component testing

## Unit testing