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

* Use arrow functions.
* Use async/await.
* Use === operator.
* Use camel case for variables, constants, functions and pascal case for classes.
* Use ESlint with appropriate plugins.
* Use only the built-in Error object or extend it. Don't extend it multiple times.
* Handle/translate exceptions in wrappers for third party libraries, API's or databases.
* Use top level error handlers to decide the appropriate action. Use lover level error handlers to add the additional context. Always use error libraries to standardize the error context.
* Document API error responses.
* Fail fast and gracefully. Use graceful degradation for API responses. If one piece of data could not be retrieved, return the rest of the response if it makes sense to do so. However, if at the time that you know the request shold fail, don't defer the responsibility to the calling object by returning null or an error object. Throw/Fail immediately. 
* Use either 500 or 200 for error responses. Advantage of using 500 is you can tell error responses by checking status only. The advantage of using 200 for errors is you can then use 500s for errors that are not because of application errors. There are examples of both in big tech companies.
* Never use console.log so you can query through logs, separate by log levels, add json objects, etc.
* Log level error only for real critical errors ie. someone needs to look at it immediately.
* Use unhandledRejection event to be able to catch unhandled promise rejections.
* Use circuit breakers to avoid cascading errors.

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