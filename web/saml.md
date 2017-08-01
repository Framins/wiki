# SAML

SAML（Security Assertion Markup Language）是一個 base on XML 的框架，同時也是一種協定。

## Terms

Roles

* User Agent
* Service Provider
* Identity Provider
* Session Participant (類似 Service Provider)

Login

![](http://www.plantuml.com/plantuml/png/XP7TQi9048NlynJdhkv5Brhx0wK8GIWAAOQiUO2mEsuMugwTsIXz-oQsGgiKRuVvliESgOKuTnGIRcVGn7jlgEIuzvRu1PCxXTmO4W6Jn9uDPMTB8rUV90Dnhr2HzKmcuU1JYxnFRQZeeoT9I15BMzu8j5v1latPqWweJv__AQSAyxRfEWgEi8aCmtH4cawo-lS1vwO1Vb175uheVBWQzQYWlGjayLgHx68Gci47BDRlnHYz_PjtMTYJGhdIQyY5PPBBW2OVmtmOz5lY7xgk2dMjrMU5jyY7XkrOuUaNs3MElW00)

```uml
@startuml
UserAgent -> ServiceProvider: (1) Access resource
ServiceProvider -> UserAgent: (2) Redirect with AuthnRequest to IdP's SSO service
IdentityProvider -> UserAgent: (3) Challenge for credentials
UserAgent -> IdentityProvider: (4) User Login
IdentityProvider -> UserAgent: (5) Signed <Response> in HTML form
UserAgent -> ServiceProvider: (6) POST signed <Response> (AssertionConsumerServiceURL)
ServiceProvider -> UserAgent: (7) Forward to resource page
@enduml
```

Logout

![](http://www.plantuml.com/plantuml/png/2qujBixCpmj8B2h9JCuiICmhKT2rK_1CISqhoIof32ZAByjCIIsoKj0mr5ImySbFpoyj2KejB4qjBh7ZGbS5qkcObr-IaLeKZ64iq0WZJ2DmAiVX2cCa8ueBylEAKx4x0wlz9fYQ0G00)

```
@startuml
SessionParticipant -> IdentityProvider: (1) <LogoutRequest>
IdentityProvider -> AnotherSessionParticipant: (2) <LogoutRequest>
AnotherSessionParticipant -> IdentityProvider: (3) <LogoutResponse>
IdentityProvider -> SessionParticipant: (4) <LogoutResponse>
@enduml
```

> Issuer: 組織單位 (Required)
>
> AssertionConsumerServiceURL: 轉向的網頁

包裝資訊的方法

* inflate
* base64 encode
* urlencode

相反地，解開的方法

* urldecode
* base64 decode
* deflate

## References

[Technical Overview](https://www.oasis-open.org/committees/download.php/27819/sstc-saml-tech-overview-2.0-cd-02.pdf)
