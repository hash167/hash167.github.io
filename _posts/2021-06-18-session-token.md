---
layout: posts
title: Authentication - Session or Token?
meta_description: auth
author: Hashim Colombowala
date: 2021-06-18 12:33:40
intro_paragraph: Authentication - Session or Token?
---

## Session Based Authentication

In this scenario, the server will create a session for the user after the user logs in. The server creates a `session id` which is stored in memory or in an external cache for horizontal scaling. The client stores the session id in a `cookie` and sends the it in the request header for every subsequent request.

```sh
Cookie: JSESSIONID=ABAD1D
```

The server can then verify the user by comparing the server id in the cookie against the session information stored in cache and responds accordingly.

![Session Auth](/assets/session_auth.png)

## Token Authentication

The server will generate a [JWT(Json Web Token)](https://en.wikipedia.org/wiki/JSON_Web_Token) with a secret and send it to the client. The client stores the JWT in a cookie or local brower memory. Subsequent requests made to server have the JWT in the header

```sh
Authorization: Bearer eyJhbGciOiJIUzI1NiIXVCJ9TJV
```

 The server validates the JWT to verify the user and respond accordingly.

![Token Auth](/assets/token_auth.png)

## Session vs Token

<u>Tokens(JWT)</u>

- Can work cross orgin across different domains. Downstream services can share tokens
- JWT based authentication scales well horizontally because tokens are stored on the client side
- Integrity protection by using a signature or MAC

<u>Sessions</u>

- More control over sessions as it is easier to invalidate. JWTs are valid till the expiration date is reached.
- If the JWT is encoded with a lot of data, it can slow down client requests. Session ids are just a string and very lightweight. Oauth2 solves this by having short lived access tokens and long lived refresh tokens


## Conclusion

In conclusion I would like to say that most production services can work with either models, so it depends on the use case. In fact many systems use a hybrid model with both types of authentication as well as combined model in which the JWT is associated with a user session for user tracking.
