# Renew Splunk server.pem Certificate

An expired certificate might cause KV Store to fail

## Set up environment variable

```bash
export SPLUNK_HOME="/opt/splunk"
```

## Check validity

```bash
openssl x509 -in /opt/splunk/etc/auth/server.pem -text -noout | grep "Not After"
```

## Stop Splunk

```bash
systemctl stop Splunkd
```

## Generate new certificate and replace the old one

```bash
$SPLUNK_HOME/bin/splunk createssl server-cert -d $SPLUNK_HOME/etc/auth -n SplunkServerDefaultCert
mv server.pem server.pem.orig
mv SplunkServerDefaultCert.pem server.pem
openssl x509 -in server.pem -text
```

## Start Splunk

```bash
systemctl start Splunkd
```
