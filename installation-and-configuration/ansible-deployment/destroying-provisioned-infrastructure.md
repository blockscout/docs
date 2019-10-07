# Destroying Provisioned Infrastructure

First, remove autoscaling groups \(ASG\) deployed via CodeDeploy manually since Terraform doesn't track them and will miss them during the automatic destroy process. Once ASG is deleted you can use the `ansible-playbook destroy.yml` playbook to remove the rest of generated infrastructure. 

Make sure to check the playbook output since in some cases it may not delete everything. Check the error description for details.

{% hint style="warning" %}
While Terraform is stateful, Ansible is stateless, so if you modify `bucket` or `dynamodb_table` variables and run `destroy.yml` or `deploy_infra.yml` playbooks, it will not alter the current S3/Dynamo resources names, but create a new resources. Moreover, altering `bucket` variable will make Terraform to forget about existing infrastructure and, as a consequence, redeploy it. If it is absolutely necessary for you to alter the S3 or DynamoDB names, perform this operation manually and then change the appropriate variable accordingly.
{% endhint %}

{% hint style="info" %}
Changing the `backend` variable will force Terraform to forget about created infrastructure, since it will start searching the current state files locally instead of remote.
{% endhint %}

