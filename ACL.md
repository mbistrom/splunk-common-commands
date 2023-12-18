# Set forwarder ACLs

```bash
apt install acl
dnf install acl
setfacl -Rm u:splunk:r-x /var/log/
setfacl -Rm u:splunk:r-x /var/log/*.log
getfacl /var/splunk/XXXX/file.log
systemctl stop SplunkForwarder.service
/opt/splunkforwarder/bin/splunk disable boot-start
/opt/splunkforwarder/bin/splunk enable boot-start -systemd-managed 1 -user splunk
chown -R splunk:splunk /opt/splunkforwarder
systemctl start SplunkForwarder.service
systemctl status SplunkForwarder.service
```
