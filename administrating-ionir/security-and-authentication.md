# Security and Authentication

For identity management, Ionir uses [OpenID Connect](https://openid.net/connect/) protocol for user identification. Any [certified OpenID Provider](https://openid.net/certification/) can be used for user authentication. As part of the installation process, Ionir installs [Keycloak](https://www.keycloak.org), an open-source identity and access management, that can be used as an identity provider (IDP) with internal users or as an identity provider (IDP) proxy, integrating with LDAP and Active Directory.

{% hint style="warning" %}
In Freemium version there is no security implemented and the **Keycloak capabilities are bypassed.**&#x20;
{% endhint %}

### Keycloak Default Credentials

Open the Keycloak UI by going to **https://\<ionir-cloud-manager-URL>/auth**&#x20;

The default Keycloak administrator user and password are set to:

<details>

<summary><strong>Keycloak Default Credentials</strong></summary>

**User**: adminidp

**Password**: adminidp

</details>

### Changing Identity Provider (IDP)

By default, each Ionir cluster uses the local Keycloak that is deployed as part of the Ionir software deployment. When connecting multiple clusters to a single Ionir Cloud all clusters in the cloud **must** use the same IDP. Similarly, when disconnecting a cluster from a Ionir Cloud it is possible to change the IDP of the cluster to the local one.

Changing the IDP is done by running a script that is provided as part of the installation process. The files that are required are:

* **README** - A readme file and an example on how to change the IDP
* **apply\_auth\_config.sh** - The script that needs to be run
* **create\_auth\_config\_file.sh** - A script that is called internally
* **authproxy.conf.template** - A configuration template

To change the cluster \[cluster A] to work with the IDP of cluster B - Run the following command:

`./apply_auth_config.sh -f authproxy -s 01a1288d-f363-4bdb-b779-bcde9367e035 -h -l https:///auth/realms/ionir -d 8.8.8.8`

For OpenShift, use the following scheme:

`./apply_auth_config.sh -f authproxy -h cluster -s 01a1288d-f363-4bdb-b779-bcde9367e035 -l /auth/realms/ionir -p <ionir route location>`

Where:

* \[cluster-A name] - is the name of the cluster that you would like to change its IDP.
* \[cluster-B ingress controller IP] - is the IP of the ingress service on the cluster that is hosting the IDP that you want to use.&#x20;

To find the IP of the ingress service, run the following `kubectl` command

`kubectl -n ionir get svc | grep ionir-nginx-ingress-controller`

To change the cluster \[cluster A] to work with its own IDP - Run the following command:

`./apply_auth_config.sh -f authproxy -s 01a1288d-f363-4bdb-b779-bcde9367e035 -h -l https:///auth/realms/ionir`

{% hint style="info" %}
**Note**: After changing the IDP of a cluster, you must log out from the Ionir Cloud Manager of the cluster and re-login.
{% endhint %}

### Ionir Cloud Manager Default Credentials

Ionir Cloud Manager users are managed using the Keycloak interface. The default Ionir Cloud Manager user and password are:

<details>

<summary>Default Credentials</summary>

**User**: admin

**Password:** admin

</details>

