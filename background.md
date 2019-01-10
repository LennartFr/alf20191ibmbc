
<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Some Background

To read:

1. [Blockchain for Developers](https://cognitiveclass.ai/learn/blockchain-for-developers/)
1. [Blockchain Essentials](https://cognitiveclass.ai/courses/blockchain-course/)
1. [IBM Blockchain Foundation Developer](https://cognitiveclass.ai/courses/ibm-blockchain-foundation-dev)

[Kevin Werbach: The Blockchain and the New Architecture of Trust. MIT Press](
https://mitpress.mit.edu/books/blockchain-and-new-architecture-trust)  


# Satoshi Nakamoto's revolution in October 2008.
 
October 2008 It all started with Satoshi Nakamoto and his paper [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf) which addressed a key problem in electronic commerce:

<img src="https://farm5.staticflickr.com/4505/24079519258_ab8a80f7ed_o.png" width="769" height="229" alt="Double Spending">
<p>
<i>
The first work on a cryptographically secured chain of blocks was described in 1991 by Stuart Haber and W. Scott Stornetta.[17] In 1992, Bayer, Haber and Stornetta incorporated Merkle trees to the design, which improved its efficiency by allowing several documents to be collected into one block.
  </i><p><i>
A blockchain database is managed autonomously using a peer-to-peer network and a distributed timestamping server. The first blockchain was conceptualised by an anonymous person or group known as Satoshi Nakamoto in 2008. 
</i><p>
https://en.wikipedia.org/wiki/Blockchain
<p>
<i>A blockchain is a decentralized virtual ledger for recording transactions <b>without central authority </b> through a distributed cryptographic protocol. 

### The Blockchain Distributed Ledger  
  
<img src="https://www.ibm.com/blogs/internet-of-things/wp-content/uploads/2017/05/2-1.jpg">
<p> 
A distributed ledger is a type of database that is shared, replicated, and synchronized among the members of a network. The distributed ledger records the transactions, such as the exchange of assets or data, among the participants in the network.

Participants in the network govern and agree by consensus on the updates to the records in the ledger. No central, third-party mediator, such as a financial institution or clearinghouse, is involved.

Every record in the distributed ledger has a timestamp and unique crytographic signature, thus making the ledger an auditable history of all transactions in the network. One implementation of distributed ledger technology is the open source Hyperledger Fabric blockchain.

	It is made up of three technologies 

1. cryptographic algorithms, 
1. a distributed protocol, 
1. and replicated data 
<p>
which combined provide a trustworthy service to a group of nodes that do not fully trust each other. 
<p>
</i>
<p>
Christian Cachin <a href="https://www.ibm.com/blogs/research/2017/10/resilient-consensus-protocols-blockchains/">Resilient Consensus Protocols for Blockchains</a>
<p>
Source: https://www.zurich.ibm.com/dccl/papers/cachin_dccl.pdf


As Vinay Gupta writes in Harvard Business Business Review of March 6 2017, [The Promise of Blockchain is a World without Middlemen](https://hbr.org/2017/03/the-promise-of-blockchain-is-a-world-without-middlemen)
	
<img src="Screen Shot 2018-10-12 at 13.05.55.png">

## Linux Foundation's Hyperledger

<img src="Screen Shot 2019-01-05 at 15.11.32.png">

## Use Cases: https://www.ibm.com/blockchain/use-cases/

## The Hyperledger components

### The Blockchain

<img src="68747470733a2f2f6661726d352e737461746963666c69636b722e636f6d2f343439362f33373833333935333439365f666130333135343133395f6f2e706e67 (1).png">

## Docker images

~~~~
1. fabric-ca
2. fabric-zookeeper
3. fabric-kafka
4. fabric-couchdb
5. fabric-javaenv
6. fabric-tools
7. fabric-ccenv
8. fabric-orderer
9. fabric-peer
10. fabric-baseimage
11. fabric-baseos
~~~~

<img src="Screen Shot 2018-10-19 at 11.49.41 (1).png">

## Message flow in a Hyperledger Fabric

<img src="fig1.png">

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

## Major components of the Hyperledger Fabric

[Hyperledger Fabric Glossary](https://fabrictestdocs.readthedocs.io/en/latest/glossary.html#hyperledger-fabric-glossary)

[Hyperledger FAQ](https://hyperledger-fabric.readthedocs.io/en/release-1.1/Fabric-FAQ.html)

<b>Hyperledger Fabric</b> is a private and permissioned blockchain without crypto-currency. Members enroll through a Membership Service Provider which calls the Hyperledger Fabric Certificate Authority which issues PKI-based 
certificates to network member organizations and their users. 

<b>Blockchain Network</b>
A blockchain network consists of, at minimum, <b>one peer</b> (responsible for endorsing and committing transactions) leveraging <b>an ordering service</b>, and a <b>membership services component (certificate authority)</b> that distributes and revokes cryptographic certificates representative of user identities and permissions.

<b>Consensus algorithm</b> is the process of reaching agreement on the next set of transactions to be added to the ledger. First a transaction must be endorsed, then passed to the Orderers for validation and commitment.  The simplest consensus algoritm is SOLO, which only needs one consenter to write transactions to the ledger.

<b>Distributed Ledger</b> The Ledger is constructed in Chaincode by the Ordering Service and is a peer-to-peer network 
of a totally ordered hashchain of blocks of (valid or invalid) transactions. The hashchain imposes the total order of blocks in a ledger and each block contains an array of totally ordered transactions. This imposes total order across all transactions.

The Distributed Ledger consists of an immutable Blockchain and the World State Database. The latter is a database containing the current value of the set of key-value pairs that have been added, modified or deleted by the set of validated and committed transactions in the blockchain.

The Ledger is kept at all peers and, optionally, at a subset of orderers. 

<b>Hyperledger Fabric channel</b> is a private “subnet” of communication between two or more specific network members, for the purpose of conducting private and confidential transactions. A channel is defined by members (organizations), anchor peers per member, the shared ledger, chaincode application(s) and the ordering service node(s).

<b>Chaincode </b> Chaincode is what Ethereum calls <b>Smart Contracts </b>. They are invoked by a client application external to the blockchain network – that manages access and modifications to a set of key-value pairs in the World State. Smart contract chaincode is installed onto peer nodes and instantiated to one or more channels.

[Chaincode and the Oracle Problem](https://medium.com/@antsankov/the-oracle-problem-isnt-a-problem-and-why-smart-contracts-makes-insurance-better-for-everyone-8c979f09851c)

<b>Peer</b> A network entity that hosts the ledger and runs chaincode containers in order to perform read/write operations to the ledger. Peers are owned and maintained by members. The number of peers required to endorse a transaction is driven by the endorsement policy that is specified at chaincode deployment time.

<b>Orderer</b> is responsible for establishing consensus. It is a defined collective of nodes that orders transactions into a block. The ordering service exists independent of the peer processes and orders transactions on a first-come-first-serve basis for all channel’s on the network. The ordering service is designed to support pluggable implementations beyond the out-of-the-box SOLO and Kafka varieties. The ordering service is a common binding for the overall network; it contains the cryptographic identity material tied to each Member.
