# Deploying BlockScout

If you are not using a Mac, skip to step 1 below.

{% hint style="warning" %}
**Mac Users Only**

To avoid the following error \(which results in a Python crash\):

`TASK [main_software : Fetch environment variables] ************************************   
objc[12816]: +[__NSPlaceholderDate initialize] may have been in progress in another thread when fork() was called.   
objc[12816]: +[__NSPlaceholderDate initialize] may have been in progress in another thread when fork() was called. We cannot safely call it or ignore it in the fork() child process. Crashing instead. Set a breakpoint on objc_initializeAfterForkError to debug.` 

1. Open terminal: `nano .bash_profile`
2. Add the following line to the end of the file: `export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES`
3. Save, exit, close terminal and re-open the terminal. Check to see that the environment variable is now set: `env`

\(source: [https://stackoverflow.com/questions/50168647/multiprocessing-causes-python-to-crash-and-gives-an-error-may-have-been-in-progr](https://stackoverflow.com/questions/50168647/multiprocessing-causes-python-to-crash-and-gives-an-error-may-have-been-in-progr)\);
{% endhint %}

1\) Ensure all [BlockScout prerequisites](../information-and-settings/requirements.md) are installed with the correct version number

2\) Create the AWS access key and secret access key for user with sufficient permissions;

3\) Create `hosts` file from `hosts.example`  \(`mv hosts.example hosts`\) and adjust to your needs. Each host should represent each BlockScout instance you want to deploy. 

{% hint style="info" %}
Each host name should belong exactly to one group. Also, as per Ansible requirements, hosts and group names should be unique.
{% endhint %}

The simplest `hosts` file with one BlockScout instance will look like:

```text
[group]host
```

Where `[group]` is a group name, which will be interpreted as a `prefix` for all created resources and `host` is a name of BlockScout instance.

4\) For each host merge `blockscout.yml.example` and `all.yml.example` config template files in `host_vars` folder into single config file with the same name as in `hosts` file:

```bash
cat host_vars/blockscout.yml.example host_vars/all.yml.example > host_vars/host.yml
```

If you have already merged `infrastructure.yml.example` and `all.yml` while deploying the BlockScout infrastructure, you can simply add the `blockscout.yml.example` to the merged file: `cat host_vars/blockscout.yml.example >> host_vars/host.yml`

5\) For each group merge `blockscout.yml.example` and `all.yml.example` config template files in `group_vars` folder into single config file with the same name as group name in `hosts` file:

```bash
cat group_vars/blockscout.yml.example group_vars/all.yml.example > group_vars/group.yml
```

If you have already merged `infrastructure.yml.example` and `all.yml` while deploying the BlockScout infrastructure, you can simply add the `blockscout.yml.example` to the merged file: `cat group_vars/blockscout.yml.example >> group_vars/host.yml`

6\) [Adjust the variables](variables.md) at `group_vars` and `host_vars`. 

{% hint style="info" %}
You can move variables between host and group vars depending on if variable should be applied to the host or to the entire group.
{% endhint %}

Also, if you need to **distribute variables across all the hosts/groups**, you can add these variables to the `group_vars/all.yml` file. 

{% hint style="success" %}
More on variable precedence =&gt; [Official Ansible Docs](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable).
{% endhint %}

7\) Run `ansible-playbook deploy_software.yml`

8\) When the prompt appears, check that server is running and there is no visual artifacts. The server will be launched at port 4000 at the same machine where you run the Ansible playbooks. If you face any errors you can either fix it or cancel the deployment by pressing **Ctrl+C** and then pressing **A** when additionally prompted.

9\) When the server is ready to be deployed simply press **enter** and deployer will upload Blockscout to the appropriate S3.

10\) Two other prompts will appear to ensure your will on updating the Parameter Store variables and deploying the BlockScout through the CodeDeploy. Both **yes** and **true** will be interpreted as the confirmation.

11\) \(optional\) If the deployment fails, you can use the following tags to repeat the particular steps of the deployment:

* build
* update\_vars
* deploy

12\) Monitor and manage your deployment at [CodeDeploy](https://console.aws.amazon.com/codesuite/codedeploy/applications) service page at AWS Console.

