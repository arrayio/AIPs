## Preamble

    AIP: <to be assigned>
    Title: Format of manifest.json DApp file
    Author: Roman Kuznetsov <Xo66uT.kr@gmail.com>
    Type: Standard track
    Category: Networking
    Status: Draft
    Created: 2018-10-04
    Dependencies: https://github.com/arrayio/array-io-client/wiki/DApp-information,-manifest.json-file

## Simple Summary
It's very important to think through and approve format of manifest.json file. Information from it will be used at DApp marketplace Smart Contract, stored at IPFS search index for marketplace and others part of Array.io ifrastructure.

## Abstract
We can divide parameters on groups:
1. Used in external systems. Such parameters as name, author_key, stored at Smart Contract.
2. Used in internal system (Array.io client). Such as index view file, main js file and others.
Why we need this separation? Because to the format of the internal parameter is affected by Client code. But when we descibes external parameters we need ti take into consideration how external systems used this parameters.

## Motivation
The motivation is simple, think it all out now so that later there are no problems. Change format in the future may cause a lot of troubles.

## Specification
### DApp information
DApp must provide information for Client application how to install it, what permissions it needed and how it showing marketplace catalog. For this conditions in the DApp archive developer must provide information file - _manifest.json_.

### About manifest.json.
The file is array dictionary, whose contents are a set of keys and values describing different aspects of the DApp. The system uses these keys and values to obtain information about your DApp and how it is configured. All information for The file contents are structured using JSON. By convention, the name of an information list file is _manifest.json_. This name of this file is case sensitive and must have an initial lowercase letter _m_. In Array.io DApps, this file resides in the top-level of the DApp archive directory.

Manifest **required** parameters:
* `name` - _varchar(30)_, uniq name for DApp, Example - "Tic Tac Toe".
* `key` - _type_, uniq key for DApp. Example - 
* `author_key` - _type_, public key for identity author of DApp. Example - 
* `version` - _varchar(5)_, current version of DApp archive. Example - "1.0.0".
* `description` - _varchar(255)_, text description what DApp do. Example - "This is a good game for all".
* `permissions` - _array_ of parameters for get access to system Controllers. Example - ["web", "log"].
* `index` - _varchar(255)_, path of DApp main view file. Example - "index.html".
* `main` - _varchar(255)_, path of DApp main js file. Example - "main.js".
* `icon` - _varchar(255)_, path of DApp main icon file. Size 42px on 42px. Example - "favicon.png".
* `thumb` - _varchar(255)_, path of DApp main thumb file. Size 300px on 120px. Example - "thumb.png".

Manifest **optional** parameters:
tags - _array_ of parameters for help search DApp at marketplace. Example - ["work", "tools"].

## Rationale
Manifest file also used in google play and app store marketplaces. We must pay attention to theirs AndroidManifest.xml and info.plist files.

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
