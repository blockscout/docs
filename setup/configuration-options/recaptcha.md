# reCAPTCHA

{% hint style="warning" %}
Blockscout currently supports **reCAPTCHA v2 in invisible mode.** Previous frontend versions (**v1.36.x)** support v3, but moving forward we will only support v2.&#x20;
{% endhint %}

reCAPTCHA from Google is a free service (with certain [usage limits](https://cloud.google.com/recaptcha/quotas)) designed to protect your site from spam and bots.  It can be used in Blockscout to prevent bot activity related to CSV downloads and account validation.  reCAPTCHA is turned on by default, but can be disabled by setting `RE_CAPTCHA_DISABLED` to true.

### Obtain your keys

1\) To use reCAPTCHA you will need a SITE KEY and SECRET KEY&#x20;

1. Go to [https://www.google.com/recaptcha/admin/create](https://www.google.com/recaptcha/admin/create), login to Google with an existing account, and fill in the following info:
   1. **Label**: Private label to identify the instance in your reCAPTCHA admin dashboard.
   2. **reCAPTCHA type**: Select Challenge (v2) and Invisible reCAPTCHA badge
   3. **Domains**: Enter your primary Blockscout domain, all associated subdomains will be covered. You can enter multiple domains, and also localhost for testing if needed.
   4. **Submit**

<figure><img src="../../.gitbook/assets/recaptcha-1.png" alt=""><figcaption></figcaption></figure>

2\) Copy your keys and use them with the following ENV variables to enable reCAPTCHA.

| Backend ENV Variable    | Google reCAPTCHA key |
| ----------------------- | -------------------- |
| `RE_CAPTCHA_SECRET_KEY` | SECRET KEY           |

| Frontend ENV Variable                 | Google reCAPTCHA key |
| ------------------------------------- | -------------------- |
| `NEXT_PUBLIC_RE_CAPTCHA_APP_SITE_KEY` | SITE KEY             |

<figure><img src="../../.gitbook/assets/recaptcha-2.png" alt=""><figcaption></figcaption></figure>

3\) Add the keys to ENV variables to your .env file or at runtime for the backend and frontend containers.\
\
Backend container:

```
$ export RE_CAPTCHA_SECRET_KEY=6Le...Qdo
```

Frontend container:&#x20;

```
$ export NEXT_PUBLIC_RE_CAPTCHA_APP_SITE_KEY=6L...IU
```

{% hint style="info" %}
Once setup, you can view and update your reCAPTCHA settings on the  Google admin dashboard at [https://www.google.com/recaptcha/admin](https://www.google.com/recaptcha/admin)
{% endhint %}

### Additional reCAPTCHA ENV info

* Backend reCAPTCHA ENVs are located in the  Backend ENVs: Common page in the [CSV exports section](../env-variables/backend-env-variables.md#csv-export).
* Frontend  reCAPTCHA ENVs are located on the Frontend ENVs: Common -> ENVs page in the [External Services section](../env-variables/frontend-common-envs/envs.md#external-services-configuration).
* Disable reCAPTCHA by setting `RE_CAPTCHA_DISABLED` to true
* Disable checking reCAPTCHA domain names by setting `RE_CAPTCHA_CHECK_HOSTNAME` to false. This will bypass checking the hostname info added during reCAPTCHA setup in Google.  [More info on domains.](https://developers.google.com/recaptcha/docs/domain_validation)
