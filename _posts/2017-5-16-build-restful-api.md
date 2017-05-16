---
layout: post
title: Build an Open API
---

## Contract is the rule

Write clear an negotiable contracts. In JS, you might use lightweight modules such as tv4[^1] and the standard JSON Schema definition[^2].

```js
const tv4 = require('tv4');

const result = tv4.validate('This is a string', { type: 'integer' });

if (result !== true) {
  console.error(tv4.error);
}
```

I have listed below the most obvious contracts having to be defined.

### Input

The most important part in the definition of the contracts is the definition of the inputs. This will engage your clients and protect yourself against bad use.

#### Parameters

- Path parameters:<br/>`/api/users/:user_id`
- Query parameters:<br/>`/api/users/:user_id?fields=name`
- Payload definition:<br/> `{type: "object", properties: { ... }}`
- Headers requirements:<br/>`Accept, Authorization, Content-Type, ...`

#### Rate

- Not more than $n$ requests per minutes
- Not more than $n$ `4xx` errors per minutes

### Output

#### Response

- Payload response must be validated:<br/> `{type: "object", properties: { ... }}`
- Headers must be validated:<br/> `Content-Type, ...`
- Response codes:<br/> `200, 202, ...`

#### Rate

- Not more than $n$ `5xx` errors per minutes

### Versioning

- Define the lifecycle of your entire API
- Allow to overwrite the lifecycle per API route
- Define clear, documented and engaged versions life times: major, minor,.<br/>*ie. **major**: 2 years, **minor**: 3 months, **patch**: 1 month* (keep delays credibility)

The RESTful API standard OpenAPI might be helpful to define the contraints listed above but keep in mind that the API you are build is yours and that you will be responsible of its maintenance as well.

## Respect the Verb

A RESTful API is build on top of HTTP verbs. Respect the verbs and use the correct ones. Isolate concerns such read and write.

## Minimum requirements

### For yourself

`HTTPS`: No serious API is available over HTTP only. Think about credentials, API keys, and possible personal and confidential data. 

`Authentication`: Which authentication will you use to authenticate your API users ? In order to have decentralized access to your API, [JWT](jwt.io) would be prefered.

`Authorization`: After having authenticated your user, check its permissions against the data you are exposing.

`IP whitelist`: for some clients, specific IPs should be used to access the API. No other referrer must be accepted.

`Secret Headers`: In order to secure your API against attackers, private secrets might be shared between customers with time based change.

`Rate Limiter`: Any Public API must have a mechanism of rate limiter per account. The rate limit must be controlled on the entire API deployment and thus, systems like [Redis](), might be used to synchronize nodes to the same value.

`Metrology`: Check real-time activity of your API with applications such as Grafana or Datadog.

`Be defensive`: Think that your users will attack you all during day. They will fall sleep on their keyboards and will start DOS you. You must defend you against internal and external clients of your API. *Don't trust anyone.*

### For your users

`Documentation`: All serious APIs have clean, understandable and stable documentation. Ensure your users can read it from anywhere (car, metro, etc.). A standard format would be chosen for the RESTful documentation such as OpenAPI (fka Swagger).

`Developer Website`: In addition to the API documentation a developers' website might be helpful. It must have clear explanations about how to register an account, how to authenticate yourself, how to access the API documentation and up-to-date real life examples.

`Sandbox`: In order to help new users to learn your API, a sandbox environment might be offered. This sandbox has a contract has any other part of the API: availability, data retention, accessibility, etc.

`Terms`: Expose to your users clear terms and conditions. This will help them deciding whether your API is suitable for their applications and if some discussions have to be planned to overcome some situations.

### For all of you

`Versioning`: An API is an Interface for a given program. By so, it must be versioned. Each time a new route is published to your users, its lifetime is guaranteed by the API contract and any change must then be backward compatible. No regression must appear without anticipated communication.

`Logging`: Keep track of API requests with correctly configured logs. Logs levels are critical because you will wake up on an `Error` but a `Warn`. Don't log useless information. Don't forget useful contextual information. Link logs all together with unique request ids.

--------------------------------------

[^1]: [tv4 - https://www.npmjs.com/package/tv4](https://www.npmjs.com/package/tv4)

[^2]: [JSON Schema](http://json-schema.org/)

[^3]: [JSON Schema](http://json-schema.org/)