# python-sslgen

python-sslgen is a Python library to generate self-signed root CA certificates, csr, sign certificates. The library enables you to manage all ssl certificates configuration in one place and create ssl certificates.

## Usage

```bash
$ sslgen <file>
```

file - ssl certificates configuration.

## Example

Example of a configuration file:

`example/ca.yaml`:

```yaml
cert:
  - name: root ca
    ca: true
    bits: 2048
    days: 365
    countryName: US
    stateOrProvinceName: Oregon
    localityName: Portland
    organizationName: test 
    organizationalUnitName: test server
    commonName: root.devel
    emailAddress: root@root.devel
    certificate: ca/ca.pem
    keyFile: ca/cakey.pem 

  - name: server
    ca: false
    bits: 2048
    days: 365
    countryName: US
    stateOrProvinceName: Oregon
    localityName: Portland
    organizationName: test 
    organizationalUnitName: test server
    commonName: server.devel
    emailAddress: root@root.devel
    certificate: server.devel/servercert.pem
    keyFile: server.devel/serverkey.pem
    csrFile: server.devel/servercert.csr
    caCertificate: ca/ca.pem
    caKeyFile: ca/cakey.pem
    subjectAltName: 
      - name: DNS.1
        value: server.devel
      - name: DNS.2
        value: www.server.devel

  - name: git
    ca: false
    bits: 2048
    days: 365
    countryName: US
    stateOrProvinceName: Oregon
    localityName: Portland
    organizationName: test 
    organizationalUnitName: test server
    commonName: git.devel
    emailAddress: root@root.devel
    certificate: git/gitcert.pem
    keyFile: git/gitkey.pem
    csrFile: git/gitcert.csr
    caCertificate: ca/ca.pem
    caKeyFile: ca/cakey.pem
    subjectAltName: 
      - name: DNS.1
        value: git.devel
      - name: DNS.2
        value: www.git.devel
```

`sslgen example/ca.yaml` creates one ca and two certificates. 
