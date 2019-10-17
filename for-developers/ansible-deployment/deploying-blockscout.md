# Deploying BlockScout

1\) Check that all [BlockScout prerequisites](prerequisites.md#infrastructure-prerequisites) are installed with the correct version number.

2\) Merge `blockscout` and `all` config template files into a single config file:

```bash
cat group_vars/blockscout.yml.example group_vars/all.yml.example > group_vars/all.yml
```

{% hint style="info" %}
All three configuration files are compatible with one another, so you can simply `cat group_vars/blockscout.yml.example >> group_vars/all.yml` if you already have the `all.yml` file after deploying the infrastructure.
{% endhint %}

3\) Set the variables at `group_vars/all.yml` config template file as described in the [variables section](variables.md).

{% hint style="info" %}
Use `chain_custom_environment` to update the variables in each deployment. Map each deployed chain with variables as they should appear at the Parameter Store. Check the example at `group_vars/blockscout.yml.example` config file. `chain_*` variables will be ignored during BlockScout software deployment.
{% endhint %}

4\) This step is for **mac OS users only**. Please skip if you are not using this OS.

To avoid the the following Python crash error:

```text
TASK [main_software : Fetch environment variables] ************************************
objc[12816]: +[__NSPlaceholderDate initialize] may have been in progress in another thread when fork() was called.
objc[12816]: +[__NSPlaceholderDate initialize] may have been in progress in another thread when fork() was called. We cannot safely call it or ignore it in the fork() child process. Crashing instead. Set a breakpoint on objc_initializeAfterForkError to debug.
```

* Open terminal: `nano .bash_profile`;
* Add the following line to the end of the file: `export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES`;
* Save, exit, close terminal and re-open the terminal. Check to see that the environment variable is now set: `env`

\(source: [https://stackoverflow.com/questions/50168647/multiprocessing-causes-python-to-crash-and-gives-an-error-may-have-been-in-progr](https://stackoverflow.com/questions/50168647/multiprocessing-causes-python-to-crash-and-gives-an-error-may-have-been-in-progr)\);

5\) Run `ansible-playbook deploy_software.yml`.

6\) When the prompt appears, check that server is running and there are no visual artifacts. The server will launch at port 4000 on the same machine where you run the Ansible playbooks. If you face any errors you can either fix or cancel the deployment by pressing **Ctrl+C** and then pressing **A** at the prompt.

7\) When the server is ready for deployment, press **enter** and deployer will upload Blockscout to the appropriate S3.

8\) Two other prompts will appear to regarding Parameter Store variables updates and deploying BlockScout through CodeDeploy. Enter **yes** and **true** to confirm.

9\) Monitor and manage your deployment at [CodeDeploy](https://console.aws.amazon.com/codesuite/codedeploy/applications) service page at AWS Console.

