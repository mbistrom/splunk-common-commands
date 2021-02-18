# Here are the steps to create your own Custom Splunk YUM/DNF repo

- Create Repo Directory mkdir /splunkrepo
- Install Nginx and set ```autoindex on;``` in nginx.conf
- Configure Nginx to use /splunkrepo as root (may have to disable SElinux ```setenforce 0```)
- Download Splunk RPM:s to /splunkrepo
- Install "createrepo" ```yum install createrepo yum-utils```
- Run ```createrepo /splunkrepo```
- Create Repo config file and distribute to Splunk servers

## Example Repo File

/etc/yum.repos.d/CentOS-Splunk.repo

```bash
[splunkrepo]
name=Splunk Software Repository
baseurl=http://FQDN-OF-REPO-SERVER/
enabled=1
gpgcheck=0
```

## Testing repo

Cleanup of temporary files

```bash
dnf clean all
```

List repos

```bash
dnf repolist
```

## Use

Install Splunk Universal Forwarder

```bash
dnf install splunkforwarder
```

Install Splunk Enterprise

```bash
dnf install splunk
```
