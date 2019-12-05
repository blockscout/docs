# Updating & Redeploying in AWS

To update to the latest version of BlockScout, or redeploy with different chain parameters, you will upload the latest version of BlockScout to your server.

1. Copy the latest version of BlockScout `git clone https://github.com/poanetwork/blockscout`
2. Zip the folder
3. Copy the zip archive to the same root application folder where the current instance resides \(this should be standard based on marketplace installation\)
4. Access the command line and stop the BlockScout service `sudo systemctl stop blockscout.service`
5. Follow the [manual deployment instructions](../manual-deployment/) starting with step 2.
6. If required, migrate the previous database following the [AWS RDS migration](https://console.aws.amazon.com/dms/) instructions.



