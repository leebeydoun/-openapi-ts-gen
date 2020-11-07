---
id: introduction
title: Introduction
sidebar_label: Introduction
slug: /
---

## What is OpenAPI TS Gen?

OpenAPI TS Gen is a [TypeScript](https://www.typescriptlang.org/) utilities library for working with API specifications
that follow the [OpenAPI Specification](https://swagger.io/specification/) (previously known as Swagger). In particular,
it provides a set of functions to create mock response JavaScript/TypeScript objects, which can be used in place of
real requests. This library is designed to work with [MSW](https://mswjs.io/docs) but can be used with other testing
frameworks.

### Example

TODO: Add example OpenAPI specification

```js
import { OAResponseGenerator } from '@openapi-ts-gen/mockgen'

new OAResponseGenerator().initialise('./sample/main-spec-file.yaml').then(gen => {
    const mock = generator('/helloWorld')
    
    console.log(mock)
})
```

### Mock Object Generation
In order to understand why this library exists, it's better to go through an example use case: 

Imagine you are using the [Testing Library](https://testing-library.com/docs/) to test some code you've written on the frontend.
You need a wait to mock out API requests made to some backend. There are a few common ways to do this:

1. Spin up a real test server that can service your front-end tests
2. Spin up a mock server based on your OpenAPI specification (for example [Prism](https://github.com/stoplightio/prism))
3. Mock the client `fetch` function (for example [Fetch Mock](http://www.wheresrhys.co.uk/fetch-mock/)) 
4. Use a Webservice Worker (for example [MSW](https://github.com/mswjs/msw))

If you spin up a full real test server, or a mock server your tests become susceptible to network failures - and in many
cases will run more slowly (simply because network requests are slow). This means the first two options are not ideal.

Mocking the client `fetch` function or using a Webservice worker are faster and can be more reliable during testing. The
problem here, **which is the problem this library is aiming to solve**, is that every single API request will
require the developer to create a custom mock.

If you have many different API requests this can be tedious. OpenAPI TS Gen, provides functions which allow you to generate
**randomised** mock response objects for any given Path defined in your `yaml` spec. 
