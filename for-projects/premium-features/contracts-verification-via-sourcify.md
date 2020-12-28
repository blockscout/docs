# Contracts verification via Sourcify

Together with contracts' verification through a flattened source file, which is a default option in Blockscout, we provide a verification option through [Sourcify](https://sourcify.dev/) tool by using their API. _Verification with Sourcify_ premium feature is enabled at [xDai instance of Blockscout](https://blockscout.com/poa/xdai).

In order to verify your contract through Sourcify tool:

   1. Open contract's address page, switch to _Code tab_ and click _Verify & Publish_ button

![](../../.gitbook/assets/screenshot-2020-12-28-at-08.38.15_2.png)

    2. Choose _Verification via sources and metadata JSON file_ option and click _Next_ button

![](../../.gitbook/assets/screenshot-2020-12-28-at-08.43.13_2.png)

As a result, you will see a form with files drop zone

![](../../.gitbook/assets/screenshot-2020-12-28-at-08.46.06.png)

3. Drag and drop all _.sol_ files used by the target contract, which you want to verify and _.json_ file with contract's metadata which created, for instance, by Truffle in _./build/contracts_ folder after `truffle compile`. If your contract has linked libraries you should also drag & drop _.json_ files __for those libraries. Instead of dragging & dropping you can also click to the button inside drop zone to invoke files popup window and chose files there. In order to initiate verification, click _Verify & Publish_ button.

![](../../.gitbook/assets/screenshot-2020-12-28-at-08.57.42_2.png)

After several seconds your contract should be verified through Sourcify's API. If verification failed, you will see a reason inside a files dropzone. In the success case, verification metadata will be saved in Blockscout DB and you will see verified contract page with the link to the same metadata in Sourcify' contract repository.

![](../../.gitbook/assets/screenshot-2020-12-28-at-08.59.50.png)

An example of [verified via Sourcify contract in Blockscout](https://blockscout.com/poa/xdai/address/0x4f15a6e74CFC2F80D5967a8aB75F3c83D8043cF4/contracts). And the same contract is in [Sourcify contract repository](https://contractrepo.komputing.org/contracts/full_match/100/0x4f15a6e74CFC2F80D5967a8aB75F3c83D8043cF4/).

