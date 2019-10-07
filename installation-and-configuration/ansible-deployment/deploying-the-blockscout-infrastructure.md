# Deploying the BlockScout Infrastructure

1. Ensure all the [infrastructure prerequisites](deploying-the-blockscout-infrastructure.md) are installed with the correct version number;
2. Create the AWS access key and secret access key for user with [sufficient permissions](aws-permissions.md);
3. Merge `infrastructure` and `all` config template files into single config file:

   ```bash
   cat group_vars/infrastructure.yml.example group_vars/all.yml.example > group_vars/all.yml
   ```

4. Set the variables at `group_vars/all.yml` config template file as described in the [variables](variables.md) section;
5. Run `ansible-playbook deploy_infra.yml`;
   * During the deployment the "[diffs didn't match](common-errors-and-questions.md#error-applying-plan-diffs-didnt-match)" error may occur. If it does, it will be ignored automatically. If the Ansible play recap shows 0 failed plays, then the deployment was successful despite the error.
   * Optionally, you may want to check the variables uploaded to the [Parameter Store](https://console.aws.amazon.com/systems-manager/parameters) on your AWS Console.

