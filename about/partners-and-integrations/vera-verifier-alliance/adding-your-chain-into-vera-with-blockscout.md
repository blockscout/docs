# Adding your Chain into Vera with Blockscout

The Vera application does not send verification requests directly to your instance, rather it stores the contract in the Verifier Alliance DB for your chain, then asks your instance to import contract details from that shared DB. The `eth-bytecode-db` service is responsible for retrieving the contract details and for contract verification.

To start:

1.  Set the correct `CHAIN_ID` value and check you are using the Blockscout hosted `eth-bytecode-db` service. To do this, specify the following ENV variables:

    ```bash
    CHAIN_ID={chain_id}
    MICROSERVICE_SC_VERIFIER_ENABLED=true
    MICROSERVICE_SC_VERIFIER_URL=https://eth-bytecode-db.services.blockscout.com/
    MICROSERVICE_SC_VERIFIER_TYPE=eth_bytecode_db

    ```

    \
    The `eth-bytecode-db` has read access to the Verifier Alliance database and can retrieve stored data.&#x20;
2. Generate an API key consisting of letters and digits and set it as the `API_SENSITIVE_ENDPOINTS_KEY` environment variable. If needed, Blockscout can generate and share it with you.This allows the Vera application service to trigger the lookup for verified contracts. \
   \
   Since contracts are not verified directly when stored in the Vera database, the instance must retrieve them for verification. Generally, the instance performs this retrieval on-demand when someone accesses the contract page. This process does not require any special access rights but has a timeout to prevent abuse. The `API_SENSITIVE_ENDPOINTS_KEY` allows the use of a special `/api/v2/import/smart-contracts/{address}` endpoint, bypassing the timeout limitation. The Vera application service uses this private endpoint to enforce the contract lookup on the instance.\
   \
   If not installed, the contract will remain unverified from the instance's point of view and will be verified later automatically when someone accesses the contract page.
3. Share the following values with Blockscout to add the chain to the Vera application(if we don't already have a shared group, [contact an admin through Discord and let them know you want to add a chain to VERA)](https://discord.gg/blockscout).
   1. Network name (e.g., Eth Mainnet)
   2. Blockscout URL (e.g., [https://eth.blockscout.com/](https://eth.blockscout.com/))
   3. `API_SENSITIVE_ENDPOINTS_KEY`
