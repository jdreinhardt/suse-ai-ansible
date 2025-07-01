# SUSE AI Ansible Install

***This is a work in progress. It doesn't check for everything, and likely has a lot of issues.***

The goal is to make an Ansible role that can be applied to stand up SUSE AI.

Create the inventory based off the included example.

Currently, only SUSE Linux Enterprise Micro 6.1 has been tested/validated.

---

`ansible.cfg` can be added to the directory for testing. This will bypass the SSH fingerprint validation.
```
[defaults]
host_key_checking = False
```

---
