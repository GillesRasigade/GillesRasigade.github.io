---
layout: post
title: Open API layer
categories:
  - software-development
date: 2018-02-07
---

Implementing Node.js Open API 3.0 specification with ease with `chpr-openapi`.

## `chpr-openapi`

OpenAPI is the last version of Swagger RESTful API contractualization: an easy and efficient way to contractualize and share your API to other guys.

A useful Node.js library, `chpr-openapi` [^1] is allowing you to add Open API specification to your Express API without having your code interweaves with external tool.

The specification is defined along your controllers and bound to your app like any other middleware. You can define the specification in the better way you decide by just creating a full JS Object validating the Open API 3.0 specification.

A secure web version of the documentation is available thanks to the amazing module ReDoc [^2]. One of the most important objective of Open API is to strictly contractualize RESTFul API and share their specifications to others. The key feature of Open API and ReDoc is to always share the most up-to-date definition of your API contract.

Forget discrepancies between `apidoc` of `jsdoc` and your API implementation. As `chpr-openapi` is validating input and output on runtime with the same contract as the documentation, you are guarantying to your clients the exact version of your API with no discrepancy risk.

The Open API 3.0 is intensively using JSON Schema [^3] implementation. Knowing these annotations will help you a lot contractualizing your objects, your API in Node.js or any other language. The module `chpr-openapi` is using `ajv`

--------------------------------------

[^1]: [chpr-openapi - https://www.npmjs.com/package/chpr-openapi](https://www.npmjs.com/package/chpr-openapi)

[^2]: [redoc - https://github.com/Rebilly/ReDoc](https://github.com/Rebilly/ReDoc)

[^3]: [JSON Schema - http://json-schema.org](http://json-schema.org/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTMwODI4OTI1XX0=
-->