#OIDC

![[Screenshot 2026-09-07 at 10.00.54.png]]

**OIDC** is an identity layer on top of OAuth2. It allows applications to authenticate users through a trusted identity provider such as Azure AD and receive signed tokens containing information about the user. This enables single sign-on and avoids applications having to manage passwords themselves.

Real-world analogy:
Imagine entering an office building.
Instead of proving who you are to every room:
1. You show your passport to reception.
2. Reception verifies you.
3. Reception gives you a visitor badge.
4. You show the badge around the building.

OAuth2 = Authorization
OIDC = Authentication

Also tokens expire.

https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/oidc-in-azure 

