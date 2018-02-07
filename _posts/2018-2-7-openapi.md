---
layout: post
title: Open API layer
categories:
  - software-development
date: 2018-02-07
---

OpenAPI is the last version of Swagger RESTful API contractualization: an easy and efficient way to contractualize and share your API to other guys.

A useful Node.js library, `chpr-openapi` [^1] is allowing you to add Open API specification to your Express API without having your code interweaved with external tool.

The specification is defined along your controllers and bound to your app like any other middleware. You can define the specification in the better way you decide by just creating a full JS Object validating the Open API 3.0 specification.

--------------------------------------

[^1]: [chpr-openapi - https://www.npmjs.com/package/chpr-openapi](https://www.npmjs.com/package/chpr-openapi)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc1MTg1MjY3NV19
-->