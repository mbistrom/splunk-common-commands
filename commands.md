# Splunk Common Commands

## Get Splunk Command BASH Completion:

```bash
source /opt/splunk/bin/setSplunkEnv
```
## Start Splunk:

```bash
splunk start
```

## Stop Splunk:

```bash
splunk stop
```

## Configure Forwarder to use a specific deplyment server:

```bash
splunk set deploy-poll <IP_address/hostname>:<management_port>
splunk restart
```
Default mamangemet port: 8089

## Reload Deployment server Apps (Stored in /opt/splunk/etc/deployment-apps):

```bash
splunk reload deploy-server
```

## Validate Indexer Cluster configuration bundle on Cluster master:

```bash
splunk validate cluster-bundle
```

## Check Indexer Cluster configuration bundle validation status om Cluster master:

```bash
splunk show cluster-bundle-status
```

## Push Indexer Cluster configuration bundle from Cluster master to indexer peers (Stored in /opt/splunk/etc/master-apps):

```bash
splunk apply cluster-bundle
```
