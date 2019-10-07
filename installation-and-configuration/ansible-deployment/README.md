---
description: Deployment with Playbooks on AWS
---

# Ansible Deployment

## Playbook Overview

We use [Ansible](https://docs.ansible.com/ansible/latest/index.html) & [Terraform](https://www.terraform.io/intro/getting-started/install.html) to build the correct infrastructure to run BlockScout.

The playbook repository is located at [https://github.com/poanetwork/blockscout-terraform](https://github.com/poanetwork/blockscout-terraform). Currently it only supports [AWS](./#using-aws-codedeploy-to-monitor-and-manage-a-blockscout-deployment) as a cloud provider.

In the root folder you will find Ansible Playbooks to create all necessary infrastructure to deploy BlockScout. The `lambda` folder also contains a set of scripts that may be useful in your BlockScout infrastructure.

1. [Deploying the Infrastructure](deploying-the-blockscout-infrastructure.md). This section describes all the steps to deploy the virtual hardware that is required for production instance of BlockScout. Skip this section if you do have an infrastructure and simply want to install or update your BlockScout. 
2. [Deploying BlockScout](deploying-blockscout.md). Follow this section to install or update your BlockScout instance.
3. [Destroying Provisioned Infrastructure](destroying-provisioned-infrastructure.md). Refer to this section if you want to destroy your BlockScout installation.

