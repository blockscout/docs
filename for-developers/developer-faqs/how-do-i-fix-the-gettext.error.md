# How do I fix the Gettext.Error?

You may receive this error after making changes to a specific BlockScout application.

`(Gettext.Error) translation with msgid '...<msg_here>...' has a non-empty msgstr`

To update gettext, run the following command **in the app’s folder where the changes were made**.

1. Go to the ./apps/{name\_of\_app} folder where the changes were made.
2. Run `mix gettext.extract —merge`
3. Repeat for other app folders as required.

More information on Gettext is [available here](https://hexdocs.pm/gettext/Mix.Tasks.Gettext.Extract.html).

{% hint style="success" %}
Content moved from [https://forum.poa.network/t/faq-fixing-gettext-error-in-blockscout/2444](https://forum.poa.network/t/faq-fixing-gettext-error-in-blockscout/2444)
{% endhint %}

