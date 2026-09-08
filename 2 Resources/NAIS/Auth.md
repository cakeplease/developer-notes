# #authentication and #authorization

**Authentication** - who are you?
**Authorization** - what do you have access to?

*Nais* helps your app with logging in users, validating inbound requests and making authenticated outbound requests using the following **identity providers**:

- #entraID -  cloud-based identity and access management service provided by Microsoft. Used for authenticating and authorizing both **employees** and **applications**

- #IDporten - (**only available in GCP**) - standard authentication service used by **Norwegian** **citizens** to access public services

- #tokenX - Nais' own implementation of OAuth 2.0 Token Exchange. Allows internal applications to act on behalf of a citizen that originally authenticated with #IDporten, while maintaining the zero trust security model between applications throughout a request chain.

- #maskinporten - service provided by DigDir used to authorize access to APIs between **organizations** or **businesses**


# Auth concepts 

## Protocols

###  #OAuth2point0
Industry-standard protocol for authorization. In NAV the protocol is used to acquire security tokens for use in authenticated requests between applications. To obtain an access token, we need an _authorization grant_. The grant represents a delegated authorization. The client application is granted authorization by a resource owner (such as an end user or the client itself) to access protected resources that belong to the owner.

### OpenID Connect ( #OIDC )
Is an identity layer on top of OAuth 2.0 protocol. See more here [[OIDC]]

### #Issuer
Defines the identifier for the provider. 

### #TokenEndpoint
Property that points to the endpoints where your client can request tokens from the provider. Tokens have a set expiration time, indicated by the expires_in field in the token response.

### #ResourceServer 
An entity that requires requests to be authenticated before responding with meaningful data. Requests to sensitive endpoints should be authenticated with a #BearerToken. The server should validate tokens for such requests before accepting or rejecting the request.

### #Client
A client or application is any entity or device that needs to get a token to access a resource server. Clients may either be public or confidential. The difference is whether the client is capable of keeping secrets. 
Backend APIs, backend-for-frontends (BFFs) or standalone daemons are typical examples of confidential clients.
Unless specified otherwise, all clients we use are confidential clients.

#### #ClientID

A client ID is a unique identifier associated with your client for a given identity provider. The value of the identifier is generally not considered to be confidential.

##### #ClientSecret
A client secret is a password that belongs to a given client. This is used to authenticate the client when attempting to acquire tokens from the identity provider.

#### #Tokens
A token is a piece of data that contains information about an authenticated entity. The receiver of a token can assert claims about the entity that the request is performed on behalf of.

An advantage of using a token is that a user never has to directly present their private credentials or passwords to the resource server. This is delegated to the identity provider who in turn issues tokens for said user. Additionally, a token often has an expiry time to limit its use.

## Workload Identity
All workloads on Nais have their own _identities_. In practice, this is a [Kubernetes Service Account](https://kubernetes.io/docs/concepts/security/service-accounts/) Workloads on Nais are automatically injected with a short-lived OpenID Connect ( #OIDC ) identity token.

### Workload identity federation
Establishes a trust relationship between the workload's identity and a third-party service.

This allows your workloads to authenticate with third-party services without the need to manage long-lived credentials, such as API keys or service account keys.
