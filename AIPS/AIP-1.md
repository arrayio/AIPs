    AIP: 1
      Title: AIP Purpose and Guidelines
      Status: Draft
      Type: Meta
      Author: Martin Becze <mb@ethereum.org>, Hudson Jameson <hudson@ethereum.org>, @Vladiuz1 (vlad@array.io)
      Created: 2015-10-27, 2017-02-01, 2018-03-17

What is an AIP?
--------------

AIP stands for Array.io Improvement Proposal. An AIP is a design document providing information to the Array.io developer community, or describing a new feature for Array.io or its processes or environment. The AIP should provide a concise technical specification of the feature and a rationale for the feature. The AIP author is responsible for building consensus within the community and documenting dissenting opinions.

AIP Rational
------------

We intend AIPs to be the primary mechanisms for proposing new features, for collecting community input on an issue, and for documenting the design decisions that have gone into Array.io. Because the AIPs are maintained as text files in a versioned repository, their revision history is the historical record of the feature proposal.

For Array.io implementers, AIPs are a convenient way to track the progress of their implementation. Ideally each implementation maintainer would list the AIPs that they have implemented. This will give end users a convenient way to know the current status of a given implementation or library.

AIP Types
---------

There are three types of AIP:

-   A **Standard Track AIP** describes any change that affects most or all Array.io implementations, such as a change to the the network protocol, a change in block or transaction validity rules, proposed application standards/conventions, or any change or addition that affects the interoperability of applications using Array.io. Furthermore Standard AIPs can be broken down into the following categories.
-   **Core** - improvements requiring a consensus fork, as well as changes that are not necessarily consensus critical but may be relevant to “core dev” discussions.
-   **Networking** - includes improvements around networking protocol. E.g. possible move to libp2p or ipfs pubsub, rpc protocol for communication of node2node, client2node.
-   **Client** - includes improvements around Array.io client specifications and standards.
-   **Interface** - improvements in language-level standards like method names and [contract ABIs]. The label “interface” aligns with the [interfaces repo] and discussion should primarily occur in that repository before an AIP is submitted to the AIPs repository.

-   An **Informational AIP** describes a Array.io design issue, or provides general guidelines or information to the Array.io community, but does not propose a new feature. Informational AIPs do not necessarily represent Array.io community consensus or a recommendation, so users and implementers are free to ignore Informational AIPs or follow their advice.
-   A **Meta AIP** describes a process surrounding Array.io or proposes a change to (or an event in) a process. Process AIPs are like Standards Track AIPs but apply to areas other than the Array.io protocol itself. They may propose an implementation, but not to Array.io's codebase; they often require community consensus; unlike Informational AIPs, they are more than recommendations, and users are typically not free to ignore them. Examples include procedures, guidelines, changes to the decision-making process, and changes to the tools or environment used in Array.io development. Any meta-AIP is also considered a Process AIP.

AIP Work Flow
-------------

The AIP repository Collaborators change the AIPs status. Please send all AIP-related email to the AIP Collaborators, which is listed under AIP Editors below. Also see AIP Editor Responsibilities & Workflow.

The AIP process begins with a new idea for Array.io. It is highly recommended that a single AIP contain a single key proposal or new idea. The more focused the AIP, the more successful it tends to be. A change to one client doesn't require an AIP; a change that affects multiple clients, or defines a standard for multiple apps to use, does. The AIP editor reserves the right to reject AIP proposals if they appear too unfocused or too broad. If in doubt, split your AIP into several well-focused ones.

Each AIP must have a champion - someone who writes the AIP using the style and format described below, shepherds the discussions in the appropriate forums, and attempts to build community consensus around the idea.

Vetting an idea publicly before going as far as writing an AIP is meant to save the potential author time. Asking the Array.io community first if an idea is original helps prevent too much time being spent on something that is guaranteed to be rejected based on prior discussions (searching the Internet does not always do the trick). It also helps to make sure the idea is applicable to the entire community and not just the author. Just because an idea sounds good to the author does not mean it will work for most people in most areas where Array.io is used. Examples of appropriate public forums to gauge interest around your AIP include [the Array.io subreddit], [the Issues section of this repository], and [one of the Array.io Gitter chat rooms]. In particular, [the Issues section of this repository] is an excellent place to discuss your proposal with the community and start creating more formalized language around your AIP. 

Once the champion has asked the Array.io community whether an idea has any chance of acceptance a draft AIP should be presented as a [pull request]. This gives the author a chance to continuously edit the draft AIP for proper formatting and quality. This also allows for further public comment and the author of the AIP to address concerns about the proposal.

If the AIP collaborators approve, the AIP editor will assign the AIP a number (generally the issue or PR number related to the AIP), label it as Standards Track, Informational, or Meta, give it status “Draft”, and add it to the git repository. The AIP editor will not unreasonably deny an AIP. Reasons for denying AIP status include duplication of effort, being technically unsound, not providing proper motivation or addressing backwards compatibility, or not in keeping with the Array.io philosophy.

Standards Track AIPs consist of three parts, a design document, implementation, and finally if warranted an update to the [formal specification]. The AIP should be reviewed and accepted before an implementation is begun, unless an implementation will aid people in studying the AIP. Standards Track AIPs must be implemented in at least three viable Array.io clients before it can be considered Final.

For an AIP to be accepted it must meet certain minimum criteria. It must be a clear and complete description of the proposed enhancement. The enhancement must represent a net improvement. The proposed implementation, if applicable, must be solid and must not complicate the protocol unduly.

Once an AIP has been accepted, the implementations must be completed. When the implementation is complete and accepted by the community, the status will be changed to “Final”.

An AIP can also be assigned status “Deferred”. The AIP author or editor can assign the AIP this status when no progress is being made on the AIP. Once an AIP is deferred, the AIP editor can re-assign it to draft status.

An AIP can also be “Rejected”. Perhaps after all is said and done it was not a good idea. It is still important to have a record of this fact.

AIPs can also be superseded by a different AIP, rendering the original obsolete.

The possible paths of the status of AIPs are as follows:

<img src=./AIP-1/process.png>

Some Informational and Process AIPs may also have a status of “Active” if they are never meant to be completed. E.g. AIP 1 (this EIP).

What belongs in a successful AIP?
---------------------------------

Each EIP should have the following parts:

-   Preamble - RFC 822 style headers containing metadata about the AIP, including the AIP number, a short descriptive title (limited to a maximum of 44 characters), the names, and optionally the contact info for each author, etc.

<!-- -->

-   Simple Summary - “If you can’t explain it simply, you don’t understand it well enough.” Provide a simplified and layman-accessible explanation of the AIP.

<!-- -->

-   Abstract - a short (~200 word) description of the technical issue being addressed.

<!-- -->

-   Motivation (*optional) - The motivation is critical for AIPs that want to change the Array.io protocol or any part of Dapp standards. It should clearly explain why the existing protocol specification is inadequate to address the problem that the AIP solves. AIP submissions without sufficient motivation may be rejected outright.

<!-- -->

-   Specification - The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Array.io platforms.

<!-- -->

-   Rationale - The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.

<!-- -->

-   Backwards Compatibility - All AIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The AIP must explain how the author proposes to deal with these incompatibilities. AIP submissions without a sufficient backwards compatibility treatise may be rejected outright.

<!-- -->

-   Test Cases - Test cases for an implementation are mandatory for AIPs that are affecting consensus changes. Other AIPs can choose to include links to test cases if applicable.

<!-- -->

-   Implementations - The implementations must be completed before any AIP is given status “Final”, but it need not be completed before the AIP is accepted. While there is merit to the approach of reaching consensus on the specification and rationale before writing code, the principle of “rough consensus and running code” is still useful when it comes to resolving many discussions of API details.

<!-- -->

-   Copyright Waiver - All AIPs must be in public domain. See the bottom of this AIP for an example copyright waiver.

AIP Formats and Templates
-------------------------

AIPs should be written in [markdown] format. Image files should be included in a subdirectory for that AIP.

AIP Header Preamble
-------------------

Each AIP must begin with an RFC 822 style header preamble. The headers must appear in the following order. Headers marked with "*" are optional and are described below. All other headers are required.

` AIP: ` <AIP number> (this is determined by the AIP editor)

` Title: `<AIP title>

` Author: `<list of author's real names and optionally, email address>

` * Discussions-To: ` <email address>

` Status: `<Draft | Active | Accepted | Deferred | Rejected | Withdrawn | Final | Superseded>

` Type: `<Standards Track (Core, Networking, Interface, ERC)  | Informational | Process>

` Created: `<date created on, in ISO 8601 (yyyy-mm-dd) format>

` * Replaces: `<AIP number>

` * Superseded-By: `<AIP number>

` * Resolution: `<url>

The Author header lists the names, and optionally the email addresses of all the authors/owners of the AIP. The format of the Author header value must be

Random J. User &lt;address@dom.ain&gt;

if the email address is included, and

Random J. User

if the email address is not given.

Note: The Resolution header is required for Standards Track AIPs only. It contains a URL that should point to an email message or other web resource where the pronouncement about the AIP is made.

While an AIP is in private discussions (usually during the initial Draft phase), a Discussions-To header will indicate the mailing list or URL where the AIP is being discussed. No Discussions-To header is necessary if the AIP is being discussed privately with the author.

The Type header specifies the type of AIP: Standards Track, Meta, or Informational. If the track is Standards please include the subcategory (core, networking, interface, or ARC).

The Created header records the date that the AIP was assigned a number. Both headers should be in yyyy-mm-dd format, e.g. 2001-08-14.

AIPs may have a Requires header, indicating the AIP numbers that this AIP depends on.

AIPs may also have a Superseded-By header indicating that an AIP has been rendered obsolete by a later document; the value is the number of the AIP that replaces the current document. The newer AIP must have a Replaces header containing the number of the AIP that it rendered obsolete.

Auxiliary Files
---------------

AIPs may include auxiliary files such as diagrams. Such files must be named AIP-XXXX-Y.ext, where “XXXX” is the AIP number, “Y” is a serial number (starting at 1), and “ext” is replaced by the actual file extension (e.g. “png”).

Transferring AIP Ownership
--------------------------

It occasionally becomes necessary to transfer ownership of AIPs to a new champion. In general, we'd like to retain the original author as a co-author of the transferred AIP, but that's really up to the original author. A good reason to transfer ownership is because the original author no longer has the time or interest in updating it or following through with the AIP process, or has fallen off the face of the 'net (i.e. is unreachable or not responding to email). A bad reason to transfer ownership is because you don't agree with the direction of the AIP. We try to build consensus around an AIP, but if that's not possible, you can always submit a competing AIP.

If you are interested in assuming ownership of an AIP, send a message asking to take over, addressed to both the original author and the AIP editor. If the original author doesn't respond to email in a timely manner, the AIP editor will make a unilateral decision (it's not like such decisions can't be reversed :).

AIP Editors
-----------

The current EIP editors are

` * Vlad Smirnov (@vladiuz1)`

` * Alexander Shevtsov (@randomlogin)`

AIP Editor Responsibilities and Workflow
--------------------------------------

For each new AIP that comes in, an editor does the following:

-   Read the AIP to check if it is ready: sound and complete. The ideas must make technical sense, even if they don't seem likely to be accepted.
-   The title should accurately describe the content.
-   Edit the AIP for language (spelling, grammar, sentence structure, etc.), markup (Github flavored Markdown), code style

If the AIP isn't ready, the editor will send it back to the author for revision, with specific instructions.

Once the AIP is ready for the repository, the AIP editor will:

-   Assign an AIP number (generally the PR number or, if preferred by the author, the Issue # if there was discussion in the Issues section of this repository about this AIP)

<!-- -->

-   Accept the corresponding pull request

<!-- -->

-   List the AIP in [README.md]

<!-- -->

-   Send a message back to the AIP author with next step.

Many AIPs are written and maintained by developers with write access to the Array.io codebase. The AIP editors monitor AIP changes, and correct any structure, grammar, spelling, or markup mistakes we see.

The editors don't pass judgment on AIPs. We merely do the administrative & editorial part.

History
-------

AIP concept was forked from Ethereum's [EIPs](https://github.com/ethereum/EIPs/) repository. In most places text was simply copied and modified.  EIP was in turn derived heavily from [Bitcoin's BIP-0001] written by Amir Taaki which in turn was derived from [Python's PEP-0001].

March 17, 2018 this document was created.

<!--
  [EIP5]: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-5.md
  [EIP101]: https://github.com/ethereum/EIPs/issues/28
  [EIP90]: https://github.com/ethereum/EIPs/issues/90
  [EIP86]: https://github.com/ethereum/EIPs/issues/86#issue-145324865
  [devp2p]: https://github.com/ethereum/wiki/wiki/%C3%90%CE%9EVp2p-Wire-Protocol
  [EIP8]: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-8.md
  [Light Ethereum Subprotocol]: https://github.com/ethereum/wiki/wiki/Light-client-protocol
  [whisper]: https://github.com/ethereum/go-ethereum/wiki/Whisper-Overview
  [swarm]: https://github.com/ethereum/go-ethereum/pull/2959
  [API/RPC]: https://github.com/ethereum/wiki/wiki/JSON-RPC
  [EIP59]: https://github.com/ethereum/EIPs/issues/59
  [EIP6]: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-6.md
  [contract ABIs]: https://github.com/ethereum/wiki/wiki/Ethereum-Contract-ABI
  [interfaces repo]: https://github.com/ethereum/interfaces
  [ERC20]: https://github.com/ethereum/EIPs/issues/20
  [ERC26]: https://github.com/ethereum/EIPs/issues/26
  [ERC137]: https://github.com/ethereum/EIPs/issues/137
  [ERC67]: https://github.com/ethereum/EIPs/issues/67
  [EIP82]: https://github.com/ethereum/EIPs/issues/82
  [EIP75]: https://github.com/ethereum/EIPs/issues/75
  [EIP85]: https://github.com/ethereum/EIPs/issues/85
  [the Ethereum subreddit]: https://www.reddit.com/r/ethereum/
  [one of the Ethereum Gitter chat rooms]: https://gitter.im/ethereum/
  [pull request]: https://github.com/ethereum/EIPs/pulls
  [formal specification]: https://github.com/ethereum/yellowpaper
  [the Issues section of this repository]: https://github.com/ethereum/EIPs/issues
  [markdown]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
-->
  [README.md]: README.md "wikilink"
  [Ethereum EIP-1]: https://github.com/ethereum/EIPs
  [Bitcoin's BIP-0001]: https://github.com/bitcoin/bips
  [Python's PEP-0001]: https://www.python.org/dev/peps/

Copyright
---------

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
