# Identity and Consent Management Examples

## Specifying Pursose

### Requesting one purpose, two scopes of the same API

#### OIDC authorization code flow
```
GET /authorize?
    response_type=code
    &scope=openid%20dpv%3AFraudPreventionAndDetection%23check-sim-swap%20dpv%3AFraudPreventionAndDetection%23retrieve-sim-swap-date
    &client_id=s6BhdRkqt3
    &state=af0ifjsldkj
    &redirect_uri=https%3A%2F%2Fclient.example.org%2Fcb HTTP/1.1
Host: server.example.com
```

#### RFC9101 request object

```
{
   "iss": "s6BhdRkqt3",
   "aud": "https://server.example.com",
   "response_type": "code",
   "client_id": "s6BhdRkqt3",
   "redirect_uri": "https://client.example.org/cb",
   "scope": "openid dpv:FraudPreventionAndDetection#check-sim-swap dpv:FraudPreventionAndDetection#retrieve-sim-swap-date",
   "state": "af0ifjsldkj",
   "nonce": "n-0S6_WzA2Mj",
   "max_age": 86400
}
```

#### [RFC7662](https://datatracker.ietf.org/doc/html/rfc7662) response on introspecting an access token issued by the above requests

```
{
      "active": true,
      "client_id": "s6BhdRkqt3",
      "username": "jdoe",
      "scope": "openid dpv:FraudPreventionAndDetection#check-sim-swap dpv:FraudPreventionAndDetection#retrieve-sim-swap-date",
      "sub": "Z5O3upPC88QrAjx00dis",
      "aud": "https://protected.example.net/resource",
      "iss": "https://server.example.com/",
      "exp": 1419356238,
      "iat": 1419350238
}
```


### Requesting two purpose, two scopes of the same API

#### OIDC authorization code flow
```
GET /authorize?
    response_type=code
    &scope=openid%20dpv%3AFraudPreventionAndDetection%23check-sim-swap%20dpv%LegitimateInterest%23retrieve-sim-swap-date
    &client_id=s6BhdRkqt3
    &state=af0ifjsldkj
    &redirect_uri=https%3A%2F%2Fclient.example.org%2Fcb HTTP/1.1
Host: server.example.com
```

#### RFC9101 request object

```
{
   "iss": "s6BhdRkqt3",
   "aud": "https://server.example.com",
   "response_type": "code",
   "client_id": "s6BhdRkqt3",
   "redirect_uri": "https://client.example.org/cb",
   "scope": "openid dpv:FraudPreventionAndDetection#check-sim-swap dpv:LegitimateInterest#retrieve-sim-swap-date",
   "state": "af0ifjsldkj",
   "nonce": "n-0S6_WzA2Mj",
   "max_age": 86400
}
```

#### [RFC7662](https://datatracker.ietf.org/doc/html/rfc7662) response on introspecting an access token issued by the above requests

```
{
      "active": true,
      "client_id": "s6BhdRkqt3",
      "username": "jdoe",
      "scope": "openid dpv:FraudPreventionAndDetection#check-sim-swap dpv:LegitimateInterest#retrieve-sim-swap-date",
      "sub": "Z5O3upPC88QrAjx00dis",
      "aud": "https://protected.example.net/resource",
      "iss": "https://server.example.com/",
      "exp": 1419356238,
      "iat": 1419350238
}
```


