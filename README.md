# SUSE AI Ansible Install

***This is a work in progress. It doesn't check for everything, and likely has a lot of issues.***

The goal is to make an Ansible role that can be applied to stand up SUSE AI.

Currently, it can be done in parts with the playbooks as they stand.

`ansible-playbook - i inventory.ini install_rke2_server.yml`

`ansible-playbook - i inventory.ini install_rancher.yml`

`ansible-playbook - i inventory.ini install_longhorn.yml`

Create the inventory and vars files based off the included examples.

---

`ansible.cfg` can be added to the directory for testing. This will bypass the SSH fingerprint validation.
```
[defaults]
host_key_checking = False
```

---

`vars.yml` explanation
```yaml
# This is used to prepare the underlying OS/make adjustments for platform specific configurations.
# Currently only rke2 is configured.
# Planned options: rke2, aks, eks, gke
system: rke2

# These are feature flags. They will install the specific options.
# rke will install RKE2 onto the hosts
# rancher will use Helm to install Rancher.
# longhorn will install OS dependencies and then use Helm to install Longhorn
install:
  rke: true
  rancher: true
  longhorn: false

# Longhorn specific options.
# default will set longhorn as the default storageclass on the cluster
# xfs will install the longhorn-xfs storageclass. Must be true for clusters
longhorn:
  default: true
  xfs: true

# These are used to provide basic starting configurations for Rancher
# hostname will be used as the Ingress point
# bootstrapPassword will be the password defined for installation. It must be changed at first used
# longhornSupport will install the OS dependencies, but not install Longhorn. This is useful if you plan to install Longhorn through Rancher
rancher:
  hostname: rancher.exmaple.com
  bootstrapPassword: admin
  longhornSupport: true
```
