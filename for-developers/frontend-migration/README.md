# Frontend Migration

The new frontend includes generalized support for L2s including views for attributes such as Index, L1 Timestamp, Size, L1 tx hash, L1 block number, and Batch root, new UI features and enhancements like the DApp marketplace and advanced statistics, and a new micro services infrastructure.

There are several options when deploying the new frontend and migrating your instance. You can either deploy in an all-in-one container, or deploy the frontend separately and connect it to the backend for more flexibility. If you have a custom backend (have made significant changes to the indexer etc) please use option 3.

1. [**All-in-one**](all-in-one-container.md): This is an easier deployment process but less flexible. It will deploy everything within a single docker container. **DO NOT use if you plan to host your frontend separately or want to make significant changes to the frontend.**
2. [**Separate frontend**](separate-frontend.md): Deploy the frontend first, then connect it to the backend. This let you make more front-end customizations, and gives you access to all images etc. **Use this method to run a separate frontend instance.**
3. [**Customized backend**](customized-backend.md): If you've customized the indexer and don't want to override it, keep your previous backend customizations and only deploy the frontend container.
