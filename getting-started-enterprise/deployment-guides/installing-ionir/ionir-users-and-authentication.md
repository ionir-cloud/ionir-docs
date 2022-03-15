# Ionir Users and Authentication

For identity management, Ionir uses [OpenID Connect](https://openid.net/connect/) protocol for user identification. Any [certified OpenID Provider](https://openid.net/certification/) can be used for user authentication. In the current version, Ionir installs [Keycloak](https://www.keycloak.org), an open-source identity and access management tool, that can be used as an identity provider (IDP) with internal users or as an identity provider (IDP) relay, integrating with LDAP.

### Keycloak Default Credentials <a href="#_heading-h.1pxezwc" id="_heading-h.1pxezwc"></a>

To login open the Keycloak UI by going to the following link:

_https://\<ionir-cloud-manager-URL>/auth_

Keycloak default administrator credentials are:

<details>

<summary>Keycloud Default Credentials</summary>

**User**: adminidp

**Password**: adminidp

</details>

****

### Ionir Cloud Manager Default Credentials <a href="#_heading-h.2p2csry" id="_heading-h.2p2csry"></a>

To login to Ionir Cloud Dashboard retrieve the nginx-ingress address with:

`kubectl get services -n ionir | grep “ionir-nginx-ingress-controller”`&#x20;

Ionir Cloud Manager default user credentials are set to:

<details>

<summary>Ionie Default Credentials</summary>

**User**: admin

**Password:** admin

</details>

****
