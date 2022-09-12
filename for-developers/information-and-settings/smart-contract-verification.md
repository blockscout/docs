---
description: Details about the verification microservice
---

# Smart Contract Verification

A microservice written in Rust provides fast and efficient contract verification. The application runs as an HTTP server and verification requests are made using REST API.

* [Basic Info](smart-contract-verification.md#basic-info)
* [Library Initialization](smart-contract-verification.md#library-initialization)
* [Solidity and Vyper Verfication](smart-contract-verification.md#solidity-and-vyper-verification)
* [Sourcify Verification](smart-contract-verification.md#sourcify-verification)
* [Verification Algorithm](smart-contract-verification.md#verification-algorithm)
* Http API

## Basic Info

### **Location**

* Application: [https://github.com/blockscout/blockscout-rs/tree/main/smart-contract-verifier](https://github.com/blockscout/blockscout-rs/tree/main/smart-contract-verifier)
* Http: [https://github.com/blockscout/blockscout-rs/tree/main/smart-contract-verifier-http](https://github.com/blockscout/blockscout-rs/tree/main/smart-contract-verifier-http)

### **Activation**

* Update Blockscout to the 4.1.8 release
* Add the following ENV variables:
  * `ENABLE_RUST_VERIFICATION_SERVICE=true`
  * `RUST_VERIFICATION_SERVICE_URL=...`  (verifier endpoint, see [http configuration](https://github.com/blockscout/blockscout-rs/tree/main/smart-contract-verifier-http) for more details)
* If running locally, the application is integrated with [`docker-compose`](https://github.com/blockscout/blockscout/tree/master/docker-compose)``

### Architecture

The service consists of 2 parts, a verification library and transport binaries that serve requests. This modular framework allows us to add new verification request protocols more easily.&#x20;

* **Verification Library**: Provides verification and a communication interface for verification functions. Includes modules for Solidity, Sourcify, and Vyper.
* **Transport Layer**: Verification requests are sent via HTTP requests.&#x20;

### Benefits

We've seen a 10X improvement in verification speed over the previous implementation. Benefits of the new microservice include:

* **Scalability**: Remove CPU intensive tasks from the primary Blockscout instance. Modularity provides the ability to scale quickly.
* **Speed**: Using native compilers greatly increases compilation speed relative to the JS wrapped versions running on Node.js used previously.
* **Improved algorithm**. New algorithm supports contracts that contain several metadata hashes, improving efficiency.

## Library Initialization

On startup, the library must retrieve all available compilers. Compiler information consists of a link to download the compiler and its hashsum \[[example](https://github.com/blockscout/solc-bin/blob/main/list.json)]. A separate thread also starts to periodically update this list.&#x20;

Library processes differ based on verification for Solidity/Vyper contracts or verification via Sourcify.

## Solidity and Vyper Verification

Verification processes are similar for contracts written in Solidity and Vyper. For Solidity contracts, verification is available for multiple files or standard json input. Single file verification is also possible, but users should verify via the multiple file method and only upload a single file.

For Vyper contracts, only multiple file verification is available.&#x20;

### Request Values

Each request contains the following values:

* Deployed bytecode: bytecode of the contract stored on chain
* Creation transaction (tx) input:  input data provided in transaction to create the contract
* Compiler version: Version of compiler used to compile the contract
* Content: Verification method related fields. E.g. for Solidity multiple files those fields are:
  * Sources: mapping from source files to their contents
  * Evm version: version of the EVM used to compile sources
  * Optimization runs: optional parameter that enables optimizations and specifies number of optimization runs
  * Contract libraries: optional parameter that specifies addresses of the contract libraries used in compiled contracts

### Verification Steps

1. **Download the compiler** with specified compiler version using the url retrieved on [initialization](smart-contract-verification.md#initialization) (or update).
2. **Compilation**: compile provided and slightly modified (see Verification Algorithm section) sources.
3.  **Verification**: compare compiler output from step 2 with bytecodes (deployed bytecode and creation tx input) provided by the caller.

    During verification all contracts obtained through local compilation are checked one by one, and if any corresponds to provided bytecodes, the verification is considered successful. Constructor arguments are also extracted
4. **Return Values**: See below.

{% hint style="info" %}
Note: available contract paths and names are obtained automatically, thus, users don’t have to specify them.
{% endhint %}

### Returned Values

As a result of successful verification the following struct is returned:

* Compiler input: Data used as an input for the compiler
* Compiler version: version of the compiler used in verification (corresponds the the version provided in request)
* File path: path of the file containing verified contract
* Contract name: name of the verified contract
* Abi: application binary interface of the verified contract ([https://docs.soliditylang.org/en/v0.8.13/abi-spec.html?highlight=abi](https://docs.soliditylang.org/en/v0.8.13/abi-spec.html?highlight=abi))
* Constructor arguments: optionally returned constructor arguments used during on chain creation of the contract.

In case of any error, enum is returned with the corresponding error and its description (e.g. if compilation failed, a Compilation error is returned with the error data obtained from the compiler).

## Sourcify Verification

The request is sent via proxy to the [Sourcify](https://sourcify.dev/) service. It accepts the following arguments:

1. Address of the contract to be verified
2. Chain id where the contract is deployed
3. Files required for Sourcify verification
4. (optionally)Contract index, if the provided files contain multiple metadata files (i.e. multiple contracts)

These arguments are sent to the Sourcify Api, which returns the verification status

### **Successful Verification**

Ether the data provided was valid and the contract was verified by them, the contract was previously verified. To obtain the actual data used in verification we send another request to retrieve source files used in verification.\
\
We expect data used for verification to be in the `metadata.json` file, so it is parsed and the information is retrieved. This includes file and contract names, compiler and evm versions, info about optimizations, contract libraries, abi, and sources.

{% hint style="info" %}
**Note**: Constructor arguments cannot currently be obtained from the metadata via Sourcify. This requires the input used for contract creation transaction and the bytecode resulting from local compilation, which are not provided.
{% endhint %}

### Failed Verification

If verification fails we return an error with description obtained from Sourcify response

## Verification Algorithm

Verification is divided into 2 parts to effectively deal with metadata hash differences in contracts. Often, very similar contracts will have very different metadata hashes based on small changes within the contract (ie an extra space in the source code). To address this, the algorithm:

1. Extracts all metadata hash fields from creation transaction input.
2. Compares non-metadata parts of the onchain bytecode with the results of local compilation.

Metadata hashes are extracted by compiling the same contract twice (with a slight modification to the 2nd contract that does not change any other part of the resultant bytecode). The resulting CreationTxInputs are compared and metadata hashes extracted by finding which parts of the inputs differ.&#x20;

### Example

An additional space in the source code can be used for the modification process. In **Example 1** and **Example 2** the only difference between both contracts is a space in the beginning of **Example 2**. However it was enough to completely change the metadata hash (metadata hash differences shown in **bold blue**).&#x20;

{% hint style="info" %}
**Note**: To update the metadata hash in production we use an additional library passed into the compiler. It does not effect the resultant bytecode, but the compilation input changes, leading to updated metadata and an updated metadata hash.
{% endhint %}

#### Example 1

```solidity
// pragma solidity ^0.8.7; contract Main {}
```

`CreationTxInput: 6080604052348015600f57600080fd5b50603f80601d6000396000f3fe6080604052600080fdfe`<mark style="color:blue;">`a264697066735822`</mark><mark style="color:blue;background-color:yellow;">**`12203cc19b771ee83d8cc6995191bd9092a82f3e66b95aacaf1cfc893d3dc27abcd2`**</mark><mark style="color:blue;">`64736f6c63430008070033`</mark>

#### Example 2

```
// pragma solidity ^0.8.7; contract Main {}
```

`CreationTxInput: 6080604052348015600f57600080fd5b50603f80601d6000396000f3fe6080604052600080fdfe`<mark style="color:blue;">`a264697066735822`</mark><mark style="color:blue;">**`1220b3902f5797f05bb62858c8d41f09402093c85957c4ae1d773e4eb1cb2000f093`**</mark><mark style="color:blue;">`64736f6c63430008070033`</mark>

### Verification Process

1. Compile the original contracts using data provided by the caller then compile those contracts again while passing in the additional library. We will get two slightly different `CreationTxInputs` if there is any encoded metadata.
2. Separate the  `MainPart` and the `MetadataPart`.
   1. &#x20;`MainPart` consists of consecutive bytes which are not related to the metadata hash (all bytes are the same for both local _CreationTxInputs_). \
      `MetadataPart` consists of consecutive bytes related to metadata hash (some bytes differ between local _CreationTxInputs_).
3.  Iterate through the two local contracts byte by byte to find the first byte that differs.&#x20;

    1. If there are no such bytes, then there is no metadata hash and the whole _creationTxInput_ consists of just one `MainPart`.
    2. If any differences are found, identify it as a hash part of the metadata hash.&#x20;
    3. Iterate back byte by byte to find the beginning of that metadata hash. When we find the beginning we know where that metadata hash starts and ends. All non-categorized bytes before the start are identified as the  `MainPart` and bytes between the start and end identified as the `MetadataPart`.
    4. Continue until there are no uncategorized bytes.





