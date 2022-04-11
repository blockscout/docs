# How do I replace missing assets/version number in my BlockScout deployment?

## Missing Assets

1. Find the public ip of corresponding Blockscout instance in the EC2 -&gt; Instances of AWS Dashboard.
2. Connect to the host via SSH `ssh -i <host.pem> ec2-user@<public_ip>`, where `<host.pem>` is host’s private key file, `<public_ip>` is the public ip of the host, that can be found in the AWS dashboard.
3. Go to assets folder `cd /opt/app/apps/block_scout_web/priv/static`
4. Add missing assets there or to `./images` folder depending on what is missing. Refresh Blockscout instance page. For example, if `favicon.ico` is missing in `./images` folder, just copy it from the root assets folder \`cp favicon.ico ./images/. You should see now the missing assets.

## Missing Version in Footer

The app version number should be in the footer of BlockScout instance

![](../../.gitbook/assets/footer1.png)

1. Find the public ip of corresponding Blockscout instance in the EC2 -&gt; Instances of AWS Dashboard
2. Connect to the host via SSH `ssh -i <host.pem> ec2-user@<public_ip>`, where `<host.pem>` is host’s private key file, `<public_ip>` is the public ip of the host, that can be found in the AWS dashboard.
3. Go to layout folder `/opt/app/apps/block_scout_web/lib/block_scout_web/templates/layout`
4. Open `_footer.html.eex` footer template in the favorite text editor. For example `nano ./_footer.html.eex` and fix the line `<% version = version() %>` \(it is in the bottom of the file\) with the hardcoded new version, for example, `<% version = 'v1.3.3-beta' %>` and save.
5. Restart the Blockscout instance with `sudo systemctl restart explorer.service`

{% hint style="success" %}
Content moved from: [https://forum.poa.network/t/faq-missing-assets-version-number-in-blockscout-deployment/2459](https://forum.poa.network/t/faq-missing-assets-version-number-in-blockscout-deployment/2459)
{% endhint %}

