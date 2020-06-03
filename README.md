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
    - [Language](#language)
    - [Error handling / logging](#error-handling--logging)
    - [Config](#config)
    - [Repos and branching](#repos-and-branching)
  - [Serverless](#serverless-1)
    - [Performance](#performance)
    - [Scaling](#scaling)
    - [Cost](#cost)
    - [Retries and error handling](#retries-and-error-handling)
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

### Language

- Use arrow functions.
- Use async/await.
- Use === operator.
- Use camel case for variables, constants, functions and pascal case for classes.
- Use ESlint with appropriate plugins.

### Error handling / logging

- Document API error responses.
- Use only the built-in Error object or extend it. Don't extend it multiple times.
- Handle/translate exceptions in wrappers for third party libraries, API's or databases.
- Use top level error handlers to decide the appropriate action. Use lover level error handlers to add the additional context. Always use error libraries to standardize the error context.
- Fail fast and gracefully. Use graceful degradation for API responses. If a non-critical piece of data could not be retrieved, return fail the whole response unnecessarily. However, if you know the request should fail, don't defer the responsibility to another object by returning null or an error object. Throw/Fail immediately.
- Use either 500 or 200 for error responses. Advantage of using 500 is the api consumer can there is an error by checking status only. The advantage of using 200 for errors is you can then use 500s for other types of errors which are separate from business logic errors. There are examples of either usage patterns in big tech companies.
- Never use _console.log_ so you can query through logs, separate by log levels, add json objects, etc.
- Log level _error_ only for real critical errors ie. someone needs to look at it immediately.
- Use _unhandledRejection_ event to be able to catch unhandled promise rejections.
- Use circuit breakers to avoid cascading errors.

### Config

- Separate config files into multiple sections or even files. This can make it easier to tell which values are used for which components.
- Separate the config values which have default values if the environment value is not there, and which values that should always be there and throw at start-up otherwise.

### Repos and branching

- Use either monorepos or polyrepos depending on use case. Monorepos have good advantages such as simpler maintenance, less switching between projects, PRs with better context, and easier code re-use.
- Use short-lived branches or trunk based development. Short lived branches enable frequent releases, conflict free merges and easy to review PRs. Trunk based development takes that a bit further and allows full continuous integration to main branch, every few minutes to a couple of hours. Trunk based development will require adopting feature toggles.
- Feature toggles should ideally be as close as to the top layer as possible, ie. web frontend, mobile client, or API interface. This will make sure the code branch is completely separate and different logical branches in the code doesn't get too complex with too many conditionals.

## Serverless

### Performance

- Run lambda benchmarks to see the optimum memory setting for your cost/speed preference.
- Use provisioned concurrency to reduce cold starts and cut down on costs on specific cases.
- Don't rely on built-in AWS SDK, or layers for that either. Bundle AWS SDK with serverless webpack and clean up your old lambda versions with automation. That way unused dependencies will not contribute to the cold starts even though they are bundled in. (eg. lambda janitor) [Read more.](https://theburningmonk.com/2019/09/should-you-pack-the-aws-sdk-in-your-deployment-artefact/)
- Lambda layers have some challenges such as running locally, testing on CI, managing changes to the layers. However they might be useful in scenarios such as layering very large dependencies to cut down on deployment times, and using custom runtimes. [Read more.](https://lumigo.io/blog/lambda-layers-when-to-use-it/)
- One trick to force a lambda cold start in the aws console is to change the environment vars.
- _lumigo-cli_ has lots of benchmark tools for cold starts and memory optimization.
- Use provisioned concurrency for strict performance requirements, stacking coldstarts or spiky traffic.
- For deployments, use weighted alias and shift the traffic gradually to the new lambda version so that provisioned concurrency can catch up. Without the weighted alias, new lambda version will serve all new requests but it'll take a few minutes for the provisioned concurrency to catch up.
- Use scheduled scaling to configure specific days or times of the day to change provisioned concurrency.
- Always enable keep-alive for lambda functions.

### Scaling

- SNS and EventBridge will trigger lambdas immediately without batching or throttling. 100 messages will trigger 100 concurrent executions.
- SQS trigger uses five pollers to long poll the queue. These pollers will burst up to 1000 pollers with increments of 60 per minute. The concurrency will increase slower compared to SNS or EventBridge.
- With Kinesis you have one execution per shard by default. With every shard, you can ingest 1mb of data or 1000 msg/second. You can also increase concurrency to process multiple batches per shard, up to 10 batches.

### Cost

- Eventbridge is twice as expensive compared to SNS and SQS per message.
- Kinesis is three times cheaper compared to SNS and SQS per message but you pay for the shar per hour. So on a large number of messages scenario, Kinesis is uncomparibly cheaper compared to other messaging services.

### Retries and error handling

- If a lambda with a kinesis trigger fails, lambda retries the batch until processing succeeds or the data expires. You can configure to retry with a smaller batch size, limit the number of retries or discard records that are too old. Discarded events can be sent to a queue or a topic as a batch.

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
