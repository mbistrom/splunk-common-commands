/opt/splunk/bin

Get Splunk Command BASH Completion:
source /opt/splunk/bin/setSplunkEnv

Start Splunk:
    splunk start

Stop Splunk:
    splunk stop

Reload Deployment server Apps (Stored in /opt/splunk/etc/deployment-apps):
    splunk reload deploy-server

Validate Indexer Cluster configuration bundle on Cluster master:
    splunk validate cluster-bundle

Check Indexer Cluster configuration bundle validation status om Cluster master:
    splunk show cluster-bundle-status

Push Indexer Cluster configuration bundle from Cluster master to indexer peers (Stored in /opt/splunk/etc/master-apps):
    splunk apply cluster-bundle
