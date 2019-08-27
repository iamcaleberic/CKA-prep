---- authentication ----
- various authentication methods include:
--- Basic ---
- Static password file
  - user - password passed as a csv file with user credentials to the api-server config using the flag -
    `--basic-auth-file=user-datails.csv`
    - the csv format is <pass>, <user>, <user-id>, <group id>
    - pass the user password in a curl command `curl -v -k https:url -u "user:password"`

- Static Token file:
  -  user - token passed as a csv file with user tokens to the api-server config using the flag -
    `--token-auth-file=user-datails.csv`
    - the csv format is <pass>, <user>, <user-id>, <group id>
    - pass the user password in a curl command `curl -v -k https:url --header "Authorization: Bearer <token>"`


--- Certificates ---
- Comms between all the kubernetes components require to be authenticated; we can use tls certificates for this
- they can be passed using two methods:
  - curl for authentication
    `curl https://url --key <client key> --cert <client cert> --cacert <ca cert>`
  - using a kubernetes Config object

--- Certificate Authority Certificate---
- To create certificates for the various components they need to be signed by a Certificate Authority (CA)
- To generate a CA certificate and key for use when generating other keys and certificates we can use openssl, cfssl, easy rsa
  - using openssl
    - generate the ca key
      `openssl genrsa -out ca.key 2048`
    - generate certificate signing request for the CA
      `openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr`
    - Self sign the certificate using x509
      `openssl x509 req -in ca.csr -signkey ca.key -out ca.crt`


---- Client certificate ---
- use the CA certificate to sign the certificates for various clients
- we can use openssl, cfssl, easy rsa
  - using openssl
    - generate the client key
      `openssl genrsa -out admin.key 2048`
    - generate certificate signing request for the client
      `openssl req -new -key admin.key -subj "/CN=kube-admin" -out admin.csr`
      Note: component certificates must be prefixed with the word `system:``
    - adding a group to the CSR
      `openssl req -new -key admin.key -subj "/CN=kube-admin/O=system:masters" -out admin.csr`
    - sign certificate with CA key
      `openssl x509 -req -in admin.csr -CA ca.cert -CAkey ca.key -out admin.crt -days 360`


--- Server certificate ---
- use the CA certificate to sign server certificates
- we can use openssl,cfssl , easy rsa
  - using openssl
    - generate key file
      `openssl genrsa -out <server>.key 2048`
    - generate CSR
      `openssl req -new -key apiserver.key -subj "/CN=kube-apiserver" -out <server>.csr`
    - to pass alternative names create an openssl cnf file [example](https://access.redhat.com/documentation/en-US/Fuse_ESB/4.4.1/html/Web_Services_Security_Guide/files/i280763.html)      
      and pass it as a config file
      `openssl req -new -key apiserver.key -subj "/CN=kube-apiserver" -out <server>.csr`
    - sign the key
      `openssl x509 -req -in <server.csr> -CA ca.crt -CAkey ca.key -out <server>.crt -days 360`


--- Certificate actions ---
- view details of certificates
  - openssl x509 -in /etc/kubernetes/pki/<certificate>.crt -text -noout



--- Certficates api ---
- you can use the inbuilt CSR object in kubernetes to sign requests and have them signed by the valid ca
- csr tasks are carried out by controller manager
  - the csr has to be added as base64 to the CSR object def file
    `cat <user>.csr | base64`
  - You can get all CSRs by:
    `kubectl get csr`
  - To approve:
    `kubectl certificate approve <name>`
  - To get the certificate:
    `kubectl get csr <user> -o yaml`
  - decode the base64 certificate
    `echo <base64 certificate> | base64 -d`
