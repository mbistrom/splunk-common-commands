# Create SSL Certificates for Splunk Web using pfSense as Certificate Authority

## Create a folder to hold the certificates
```
mkdir $SPLUNK_HOME/etc/auth/mycerts
cd $SPLUNK_HOME/etc/auth/mycerts
```
## Generate key with password
```
$SPLUNK_HOME/bin/splunk cmd openssl genrsa -des3 -out mySplunkWebPrivateKey.key 2048
```
## Remove password from key 
```
$SPLUNK_HOME/bin/splunk cmd openssl rsa -in mySplunkWebPrivateKey.key -out mySplunkWebPrivateKey.key
```
## Create a Certificate Signing Request using the passwordless key
```
$SPLUNK_HOME/bin/splunk cmd openssl req -new -key mySplunkWebPrivateKey.key -out mySplunkWebCert.csr
```
## Use the CSR to create a signed certificate on pfSense
System -> Cert. Manager 

Certificates -> Add/Sign

Method: Sign a Certificate Signing Request

CSR data: \<paste contents of CSR\>

Certificate Lifetime (days): 825
(Limited by https://support.apple.com/en-us/HT210176)

Digest Algorithm: sha512

Certificate Type: Server Certificate

Alternative Names -> FQDN or Hostname: \<FQDN of the Splunk Web server\>

Save 

## Export the newly created certificate
Save as mySplunkWebCert.crt

## Export the CA certificate
Save as myCACert.crt

## Convert both to PEM-format
```
splunk cmd openssl x509 -in myCACert.crt -out myCACert.pem -outform PEM
splunk cmd openssl x509 -in mySplunkWebCert.crt -out mySplunkWebCert.pem -outform PEM
```
## Concatenate both files to one
```
cat mySplunkWebCert.pem myCACert.pem > mySplunkWebCertificate.pem
```
## Edit $SPLUNK_HOME/etc/system/local/web.conf
Add to the [settings] stanza: 
```
enableSplunkWebSSL = true
privKeyPath = /opt/splunk/etc/auth/mycerts/mySplunkWebPrivateKey.key
serverCert = /opt/splunk/etc/auth/mycerts/mySplunkWebCertificate.pem
```

# Restart Splunk 
```
$SPLUNK_HOME/bin/splunk restart splunkd
```
