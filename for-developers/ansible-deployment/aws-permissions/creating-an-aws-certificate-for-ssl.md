---
description: Optional process if you want to use SSL with your BlockScout instance
---

# Creating an AWS certificate for SSL

{% hint style="warning" %}
If you **do not want to use SSL**, you can disable by adding the `use_ssl = "false"` parameter to the `terraform.tfvars` file.
{% endhint %}

### To create:

1\) Go to [https://console.aws.amazon.com/acm/](https://console.aws.amazon.com/acm/). Select provision certificates and click on get started:

![Get Started](../../../.gitbook/assets/get_started.png)

2\) Request a Public Certificate.

![Request a certificate](../../../.gitbook/assets/request.png)

3\) Add a domain you have access to and click **Next**.

{% hint style="info" %}
This does not need to be the same domain for deployment - as long as it’s a valid ARN on your account it will pass verification.
{% endhint %}

![Add your Domain name](../../../.gitbook/assets/next.png)

4\) Choose your validation method \(your preference\) and click **Review**.

![Choose either method and click Review](../../../.gitbook/assets/review.png)

5\) Review your information and click **Confirm and request.**

![Click Confirm and request](../../../.gitbook/assets/review2.png)

6\) Click **Continue** to begin validation.

![Continue to Validate your certificate](../../../.gitbook/assets/validate.png)

7\) Confirm the Domain:

* **DNS Validation:** Create a CNAME record in the DNS configuration for each of the domains listed below.
* **Email Validation:** Receive email and follow link

![Email Validation](../../../.gitbook/assets/email.png)

8\)  Approve the Certificate

![Click I Approve to complete the process](../../../.gitbook/assets/approve.png)

9\) In the AWS Certificate Manager, click on the domain name to view the certificate details. **Copy and paste your ARN** into the `alb_certificate_arn` field in the `terraform.tfvars` file 

![Copy and Paste the full ARN into the alb\_certificate\_arn field in terraform.tfvars](../../../.gitbook/assets/copy_arn.png)

