openshift_aws_cleanup
=====================

Cleanup AWS resources created by OpenShift 4 installations where cluster uninstall can not be used.

This role finds and deletes a number of different types of AWS resources.
While it has been well tested, we must emphasize that this sort of find-and-delete activity is inherently dangerous.
Using `openshift-install destroy cluster` is the recommended way to remove a cluster and related AWS resources.
This role is meant only for clean up when this is not an option.

Requirements
------------

`aws` command line utility authenticated to an AWS account.

Role Variables
--------------

`openshift_aws_cleanup_cluster_ids` - List of OpenShift cluster IDs.
IDs will be matched against AWS resource tags `kubernetes.io/cluster/<ID>` and should include the full id, ex: `cluster-example-4a4ax`.

`openshift_aws_cleanup_region` - Region to clean resources from. Each run of this role cleans one region.

Example Playbook
----------------

An example playbook is included with the role:

```
- name: Clean-up AWS For cluster
  hosts: localhost
  roles:
  - openshift_aws_cleanup
```

An example `vars.yaml` file:

```
openshift_aws_cleanup_region: us-east-1
openshift_aws_cleanup_cluster_ids:
- cluster-test01-q2245
- cluster-test02-x945a
- cluster-test03-ah8a6
```

Run with:

```
ansible-playbook playbook.yaml -e @vars.yaml
```

License
-------

GPLv3

Author Information
------------------

Johnathan Kupferer
