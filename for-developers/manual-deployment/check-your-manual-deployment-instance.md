# Check your Manual Deployment Instance

1. Check that there are no visual artifacts, all assets exist and there are no database errors.
2. If there are no errors, stop BlockScout \(`ctrl+c`\)
3. Build static assets for deployment `mix phx.digest`
4. Delete build artifacts:

   a. Script: `./rel/commands/clear_build.sh`

   b. Manually:

   * delete `_build` & `deps` directories
   * delete node modules located at
   * `apps/block_scout_web/assets/node_modules`
   * & `apps/explorer/node_modules`
   * delete `logs/dev` directory

