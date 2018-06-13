    AIP: 1
      Title: Dapp Registry
      Status: Draft
      Type: Meta
      Author: @Vladiuz1 (vlad@array.io)
      Created: 2018-06-13

What is Dapp Registry?
--------------

Dapp registry is a registrar of dapp bundles published or unpublished.

Rationale
---------

A Dapp needs 3 fundamental features:

1. Author verificiation
2. A unique name
3. Versioning system
4. A place with a list of all dapps

The Dapp registry will take care of these tasks.

Description
-----------

The Dapp registry will be implemented by a smartcoctract within Array.io core blockchain.

This smart contract will be responsible for registering new dapp names, with reference to dapp determenistic hash. Both the hash and the name will be used by Array.io-client as keys for referencing an installed app.

The regitry smart contract will make sure that the name is unique. And will also contain the default language of the name. It will also assign an author during registration of the name of a dapp. The author will be identified by account (or address) that has submited name registration request. The author can theoretically be a smart contract.. A multisig for example.

Versioning is another feature of the smart contract. Every new version will be submited to the smart contract, identifying the author (account or address) making sure he has authority over the app, and the registry will assign a new address of the dapp.

Execution of registered and unregistered apps may be allowed/forbidden on the client settings level. If user of client application allows execution of unregistered apps, he will get a warning trying to execute such application, yet it will let her/him execute it. Similar to how osx manages its securities policies regarding what code is allowed to be executed.

Registry must also have transfer ownership functionality.

A smart contract is the easiest way to manage such registry for a few reasons.

Definitions
-----------

*Author* - an entity/person that created the dapp, and registered its name within Dapp Registry smart contract. Author is identified by the account that has current author rights.

*Hash* - deterministic hash based on dapp bundle content. Based on IPFS. Also used to identify a version of the dapp. It is also part of IPFS address if the dapp is published on the network.

*Name* - user friendly name of the dapp.

*Version* - a userfriendly version of the dapp described here: https://github.com/arrayio/array-io-client/issues/14. Every version has its own address in the IPFS (hash).
