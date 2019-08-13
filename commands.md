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
