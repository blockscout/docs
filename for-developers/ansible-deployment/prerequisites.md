# Prerequisites

Playbooks rely on Terraform, the stateful infrastructure-as-a-code software tool. It allows you to modify and recreate single and multiple resources depending on your needs.

This version of playbooks supports the multi-hosts deployment, which means that test BlockScout instances can be built on remote machines. In that case, you will need to have the Ansible, installed on jumpbox \(controller\) and all the prerequisites described below, installed on runners.

### Infrastructure Prerequisites

| Dependency name | Installation method |
| :--- | :--- |
| Terraform &gt;=0.11.11 &lt;= 0.11.14 | [Installation guide](https://learn.hashicorp.com/terraform/getting-started/install.html) |
| Python 3 | `apt install python3.7` |
| Python3-pip | `apt install python3-pip` |
| Ansible &gt;=2.8.x | `pip3 install ansible` |
| boto & boto3 & botocore python 3 modules | `pip3 install boto boto3 botocore` |

### BlockScout Prerequisites

| Dependency name | Installation method |
| :--- | :--- |
| Terraform &gt;=0.11 &lt;= 0.11.14 | [Installation guide](https://learn.hashicorp.com/terraform/getting-started/install.html) |
| Python 3 | `apt install python3.7` |
| Python3-pip | `apt install python3-pip` |
| Ansible &gt;=2.8.x | `pip3 install ansible` |
| boto & boto3 & botocore python modules | `pip3 install boto boto3 botocore` |
| AWS CLI | `pip3 install awscli` |
| All BlockScout prerequisites | [See BlockScout Requirements](../information-and-settings/requirements.md) |

