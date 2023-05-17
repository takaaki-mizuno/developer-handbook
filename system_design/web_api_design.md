# Web API Design

## JSON over HTTP API vs GraphQL

The choice between JSON over HTTP API and GraphQL depends on the specific needs of your project.

- If we need to provide the API to third-party developers, we should use JSON over HTTP API. Because it is easier to understand and use.
- In other cases, we should use JSON over HTTP API as a primary choice because it is more simple.
- We can use GraphQL when the application has complex, deeply nested data structures.

## Authentication / Authorization

There are two possible patterns for the authentication/authorization used in APIs. One is a type of API that is called by other services and systems, just like AWS, and the other is an API that is called directly by end-users, like a mobile backend.

The required authentication mechanism should be different for each type.

### API for other services and systems

In APIs called from other services, authentication is performed using the API Key. In other words, just as in AWS authentication, an Access ID and Access Secret are issued to authenticate.

This is because there is no reason to go through the time-consuming process of obtaining an access token using an ID and password since the service being accessed needs to keep the authentication information within the service anyway.

One Access ID can be issued for each user, or multiple Access IDs can be issued. In addition, Access Secret should be able be changed by service admins at any time on the management screen so that countermeasures can be taken immediately in case of information leakage.

Services that use the API should put the API Key in the request header and send it with Authorization: Bearer xxx.

### API for end-users

APIs that end-users call directly uses user ID (usually an email address) and password for authentication.

In this case, the OAuth2 Password Grant is used. The authentication endpoint should be as follows.

| Endpoint              | Description                       |
|-----------------------|-----------------------------------|
| /auth/token           | Get access token                  |
| /auth/token           | Refresh token                     |
| /auth/password/forgot | Generate token for reset password |
| /auth/password/reset  | Reset password                    |


