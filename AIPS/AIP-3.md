---
aip: 3
title: ARC3 - Dapp Registry Smart Contract
author: @vladiuz1 <vs@array.io>
type: Standards Track
category: ARC
status: Draft
created: 2018-06-13
dependencies: -
---

What is Dapp Registry?
--------------

Dapp registry is a registrar of dapp bundles published or unpublished.

Rationale
---------

A Dapp needs a few fundamental features:

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


Functionality
-------------

### Registering a dapp name.

Our dapp names will be part of URI addresses used to reference a dapp or an anchor within a dapp. Hence the dapp names must be unique. In order to provide such uniqness, we must devise a system how to assign a unque name to a dapp. Just like with domains, we anticipate that there may be demand for good application names, and many users may wish to compete for a good dapp name. Proposed smart contract functionality allows for charging a fee for registering a name. This solves a problem of mass registering the names.

Even a small fee will ensure that there is a way to limit the amount of reserved names.

Every dapp name must be a ERC721 token, ownership of which can be passed over to other authors. Early registrators of the names, will obviously have edge, but they also risk to loose their investment, and there will be registration fee.

Since registering a name may be done in a decentralized way, we need to make sure that nodes that propagate registration request do no hijack registration and register a good name just before an author trying to register a name or merely looks up a name for uniqueness in a smart contract.

This is achieved by name reservation. This is how i propose it shall work:

1. Download a list of all names from the registry.
2. Check your name for unqueness locally (do not send to a public node).

If you are connected to a private node, you can just query your node smart contract method (`search(name).call()`) to find if a name has been registered before.

3. Execute a smart contract method `reserve(namehash).execute()` with your author account. Where namehash is a ripemd160 hash of a `concat(name, account, salt)` that you, as author have generated locally. This is a safe proof that you were the first who registered the name. Here name - the name you are trying to register, account - your author account, and salt - is a random secret that only you know.

4. After this function has been irreversably accepted by the blockchain, it is safe to send the name registration with name unencrypted. So after a few blocks generated you will send another method call:
`register(name, defaultLanguage, salt, version, ipfsHash)`. This checks name against a duplicate registration if there is no previously registered dapp with that name, it is automatically minted (erc721 token, remember?) and ownership passed to the you.

If there is a recent registration of that name, then the registry smart contract calculates both your namehash and previously registered author's namehash, locates both `reserve()` records, and if your reservation was submitted before the other author's name reservation, it automatically passes the ownership of that name erc721 token to you BUT provided that your `reserve()` hasn't expired. 

We must invalidate `reserve()` after a short period of time (say few hours) to avoid mass hidden pre registrations. So that the open database of already registered names reflected the most relevant list of unque names.

Using erc721 standart for dapp names, is pretty much equals to ownership of dapps, erc721 includes all the functionality that allows quick passing of ownership (authorship) of dapp names.

Whoever invests enough amount of RAY into dapp name registration receives a bonus of ability to sell these names in a free market.

### Author verification

This is the easiest part. 

Since we use erc721, we implement 2 more methods on top of standard erc721 method (`ownerOf`):

```javascript
function ownerOfName(string name) external view returns (account)
```
and
```javascript
function ownerOfHash(string hash) external view returns (account)
```
So you can lookup ownership by `hash` and by `name`, on top of `tokenId`

## List of methods

```solidity
/// the dapp registry interface extends ERC721 interface
interface AIP3 is ERC721 {
    
    /// @notice reserves a name using namehash
    /// @param namhash - is a hash of name+account+salt
    function reserve(bytes32 namehash) external;
    
    /// @notice register a new unique name of dapp.
    /// @dev this function registers a new name (if it has not been registered before)
    /// and assigns a version and bundle hash to it.
    /// if this name is taken, it checks if recent `reserve()` with namehash has
    /// was the first one to attempt pre registration. If it was, it transfers the ownership
    /// to this author.
    /// @param name - the utf-8 name of the dapp.
    /// @param locale - the language code of the name, e.g. ru_RU.
    /// @param version - the first version of the app (e.g. 0.1.0) compliant with https://github.com/arrayio/array-io-client/issues/14
    /// @param ipfsHash - the hash of the dapp bundle
    /// @param salt - the salt used to create `reserve` namehash
    function register(string name, string language, string version, bytes ipfsHash, bytes salt) external payable;
    
    /// @notice publish a new version of already registered dapp.
    /// @param tokenId - the token id
    /// @param version - the new version of the app compliant with https://github.com/arrayio/array-io-client/issues/14
    /// @param ipfsHash - the hash of the dapp bundle
    function update(uint256 tokenId, string version, bytes ipfsHash) external onlyOwner payable;
    
    /// @notice there should be no name change allowed. Just register a new one and 
    /// publish a new version.
    /// function changeName();

    /// @notice lookup if a name is available
    /// @param name - the name to check for availability
    /// @warning MUST BE USED ONLY WITH TRUSTED NODES!!!
    function lookup(string name) external view returns (bool available);


    /// @notice owner of the dapp identified by name
    /// @param name - the unique name of the dapp
    function ownerOfName(string name) external view returns (account owner);
    
    /// @notice owner of the dapp identified by hash
    /// @param hash - the deterministic IPFS hash of the dapp
    function ownerOfHash(bytes32 hash) external view returns (account owner);
    
    /// @notice get tokenId by dapp name
    /// @param name - the unique name of the dapp
    function idByName(string name) external view returns (uint256 tokenId);
    
    /// @notice get tokenId by IPFS hash
    /// @param hash - the deterministic IPFS hash of the dapp
    function idByHash(bytes32 hash) external view returns (uint256 tokenId);

      /// @notice get dapp name given an IPFS hash
      /// @param hash - the ipfs hash (address)
      function nameByHash(bytes32 hash) external view returns (string name);

      /// @notice get IPFS hash given dapp name
      /// @dev returns the hash of the last verions of the dapp given the name
      /// @param name - unique name of the dapp
      function hashByName(string name) external view returns (bytes32 hash);

      /// @notice get IPFS hash given both a dapp name and a version
      /// @dev returns the hash of the dapp given both the version and the name
      /// @param name - unique name of the dapp
      /// @param version - the version of the dapp
      function hashByNameVersion(string name, string version) external view returns (bytes32 hash);

      /// @notice get latest version of dapp given its name
      /// @param name - unique name of the dapp
      function versionHashByName(string name) external view returns (string version, bytes32 hash);

      /// @notice get latest version of dapp given dapp's IPFS hash
      /// @param hash - the ipfs hash (address)
      /// @returns - version of the app given the IPFS hash of the dapp bundle
      function versionByHash(bytes32 hash) external view returns (string version);

      /// @notice get the language of the name registered
      /// @param name - unique name of the dapp
      function languageByName(string name) external view returns (bytes5 language);    
    
    
    }
```

Other uses
----------

DApp registry may also be used for other use cases where unique naming is required.

For example, let's say you are making a distributed Web brwoser based on Array.io or any front end client for IPFS. You need a decentralized domain name registry. Userfriendly domain name shortcuts would be an obvious usability shortcut to memorize addresses in IPFS. The same smart contract may be used for this.

One of ideas we have is a ipfs-based markdown editor (let's say array://wiki/) that will create a distributed and decentralized wikipedia residing in IPFS. Editing a wiki entry will be built into a viewer, everytime a user saves edited page (let's say array://wiki/Steven_Hawking), naturally its IPFS address changes. Once the user is ready to commit the change, he is executing an 'update' method of the name registry contract pointing the name 'Isaak_Newton' to new IPFS address.

Similarly one could create a distributed github with unique naming/version registry.
