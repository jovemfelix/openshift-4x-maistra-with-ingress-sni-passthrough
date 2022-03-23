# Variables

```shell
APP=teste5
SA=${APP}-sa
SVC=${APP}-svc
NS=redhat-${APP}
SECRET=${APP}-credential
DOMAIN=example.com
H=${APP}.${DOMAIN}
GW=${APP}-gw
VS=${APP}-vs
INGRESS_HOST=172.23.216.3
SECURE_INGRESS_PORT=443
```



# Generate client and server certificates and keys

```shell
# For this task you can use your favorite tool to generate certificates and keys. The commands below use openssl
# Create a root certificate and private key to sign the certificate for your services:

$ openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -subj "/O=ca-organization/CN=${DOMAIN}" -keyout ${DOMAIN}.key -out ${DOMAIN}.crt

# Check a certificate and return information about it (signing authority, expiration date, etc.):
$ openssl x509 -in ${DOMAIN}.crt -text -noout

# Check the SSL key and verify the consistency:
$ openssl rsa -in ${DOMAIN}.key -check


# Create a certificate and a private key for nginx.example.com:
$ openssl req -out ${H}.csr -newkey rsa:2048 -nodes -keyout ${H}.key -subj "/O=${APP}/CN=${H}"

$ openssl x509 -req -days 365 -CA ${DOMAIN}.crt -CAkey ${DOMAIN}.key -set_serial 0 -in ${H}.csr -out ${H}.crt

```

# Deploy an NGINX server

```shell



```

# Reference
* https://istio.io/v1.9/docs/tasks/traffic-management/ingress/ingress-sni-passthrough/