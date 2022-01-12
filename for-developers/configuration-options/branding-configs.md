# Branding Configs

{% hint style="warning" %}
This page is currently in development. See the [ENV Variables page](../information-and-settings/env-variables.md) for more info on specific variables mentioned below.
{% endhint %}

{% hint style="info" %}
Note: if you've previously deployed and are updating your BlockScout version with new assets, be sure to remove static assets from the previous build (use `mix phx.digest.clean`or manually delete assets located in _apps/block\_scout\_web/priv/static_ folder) before updating current files and restarting/rebuilding BlockScout.&#x20;

In order to rebuild new front-end assets run:

1. `cd apps/block_scout_web/assets; npm install && node_modules/webpack/bin/webpack.js --mode production; cd -`
2. `mix phx.digest`
{% endhint %}

1. **Theme Colors and other CSS-based attributes**: See [CSS Configs and Presets](css-configuration-and-presets.md) to set your instance to the stylesheet you want to use.
2. **Logos**: Use the LOGO and **** LOGO\_FOOTER [env variables](../information-and-settings/env-variables.md) to direct to your uploaded logos. Logos and other assets are located in the `apps/block_scout_web/assets/static/images` folder.
3. **Coin**: [Customize the coin symbol ](../../for-users/faqs/how-can-i-customize-the-coin-symbol.md)using the COIN  & COINGECKO\_COIN\_ID [env variables](../information-and-settings/env-variables.md).
4. **MetaData**: MetaTags can be adjusted for various pages in the templates area. For the home page, tag data is rendered from here: `/apps/block_scout_web/lib/block_scout_web/templates/chain/_metatags.html.eex`
5. **Titles / Subtitles**: Browser tab displays the title from the 2 SUBNETWORK + NETWORK [env variables](../information-and-settings/env-variables.md).
6. **Favicon**: replace the current favicons located in the `apps/block_scout_web/assets/static/images` folder.
7. **Menus**: Use the APPS\_MENU **** [env variable](../information-and-settings/env-variables.md) to include an apps menu and **** EXTERNAL\_APPS **** to populate the menu.
8.  **Top navigation bar**: Data is rendered from here:

    `/apps/block_scout_web/lib/block_scout_web/templates/layout/_topnav.html.eex`
9. **Footer**: Data is rendered from here: `/apps/block_scout_web/lib/block_scout_web/templates/layout/_footer.html.eex`
10. **Custom Theming**: Custom theming is available from the BlockScout team. [Learn More](../../for-projects/premium-features/custom-branded-themes.md).





