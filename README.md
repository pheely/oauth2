# OAuth2

## 1. OAuth2 Roles
OAuth2 defines four roles:

1) resource owner:
Could be you. An entity capable of granting access to a protected resource. When the resource owner is a person, it is referred to as an end-user.

2) resource server:
The server hosting the protected resources, capable of accepting and responding to protected resource requests using access tokens.

3) client:
An application making protected resource requests on behalf of the resource owner and with its authorization. It could be a mobile app asking your permission to access your Facebook feeds, a REST client trying to access REST API, a web site [Stackoverflow e.g.] providing an alternative login option using Facebook account.

4) authorization server:
The server issuing access tokens to the client after successfully authenticating the resource owner and obtaining authorization.
