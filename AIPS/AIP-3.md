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

