# Backup Kubernetes etcd

> 💀 DANGER:  This script *only* creates a backup of the etcd portion of
> a Kubernetes cluster as created with `kubeadm init`. Backing up
> applications with any persistent data within the cluster is not
> included. Mileage may vary. You assume the risk of running it.
> (Consider Velero for full disaster recovery.)

## Assumptions and Requirements

* Written in bash with `shellcheck` validation
* Default `kubeadm init` used to create
* "Stacked" or "external" etcd must be supported
* Must not depend on containers or Kubernetes to run
* Multiple cluster backups saved near one another over NAS
* Delete backups older than a specific number of days
* Base age of backups on ISO 8601 timestamps in file name
* No dependency on last modified time of file itself
* Redundant backups saved to different target locations/filesystems
* Consistent output compatible with monitoring systems (like Icinga2)
* Use OK (0), WARNING (1), CRITICAL (2) for standard output with message
* Must immediately exit on failure during any part of script
* Must support execution from system cron
* Must support execution from alert system scheduler (like Icinga2)
* Must support ad hoc execution outside of regular schedule
* Must validate the snapshot backup file generated
* Must support ETCD API 3
* Must only save snapshot of current "leader"
* Must take zero arguments (all configuration hard-coded in script)
* Must be testable

## Related

* How To Backup Etcd And Restore It On Kubernetes Cluster  
  https://devopscube.com/backup-etcd-restore-kubernetes/
