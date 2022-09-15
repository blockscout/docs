# How do I update the UI?

See the [Branding configs](../configuration-options/branding-configs.md) page for details related to different UI elements.&#x20;

For updates like adding elements/links etc you will need to change .eex templates. When changing .eex templates you don't need to rebuild. Run the application in dev mode (MIX\_ENV=dev), and change the template. You'll see changes on-the-fly. When chaging js/scss while running the application, you need to run `mix phx.digest` to apply the changes.
