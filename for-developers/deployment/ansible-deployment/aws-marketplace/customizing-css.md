# Customizing CSS

If you would like to customize the theme, follow these steps after a successful deployment:

1. ssh in and stop the BlockScout service:\
   `sudo systemctl stop blockscout.service`\

2. Navigate to `blockscout/apps/block_scout_web/assets/css/theme`.\

3. Edit `_poa_variables.scss` with appropriate theme colors.\

4. Rebuild the static assets: `sudo npm run-script deploy` (from blockscout/apps/block\_scout\_web/assets directory).\

5. Restart the BlockScout service:\
   `sudo systemctl start blockscout.service`

The BlockScout application will now be running with the designated theme changes.\
