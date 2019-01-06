<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# The Workshop

## How did it all start?

October 2008 It all started with Satoshi Nakamoto and his paper [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf) which addressed a key problem in electronic commerce:

<img src="https://farm5.staticflickr.com/4505/24079519258_ab8a80f7ed_o.png" width="769" height="229" alt="Double Spending">

## Linux Foundation's Hyperledger

<img src="Screen Shot 2019-01-05 at 15.11.32.png">

## Use Cases: https://www.ibm.com/blockchain/use-cases/

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

## The Hyperledger components

<img src="68747470733a2f2f6661726d352e737461746963666c69636b722e636f6d2f343439362f33373833333935333439365f666130333135343133395f6f2e706e67 (1).png">

<img src="Screen Shot 2018-10-19 at 11.49.41 (1).png">

<b>Distributed Ledger</b> The Ledger is constructed in Chaincode by the Ordering Service and is a peer-to-peer network 
of a totally ordered hashchain of blocks of (valid or invalid) transactions. The hashchain imposes the total order of blocks in a ledger and each block contains an array of totally ordered transactions. This imposes total order across all transactions.

The Distributed Ledger consists of an immutable Blockchain and the World State Database. The latter is a database containing the current value of the set of key-value pairs that have been added, modified or deleted by the set of validated and committed transactions in the blockchain.

The Ledger is kept at all peers and, optionally, at a subset of orderers. 

<b>Hyperledger Fabric channel</b> is a private “subnet” of communication between two or more specific network members, for the purpose of conducting private and confidential transactions. A channel is defined by members (organizations), anchor peers per member, the shared ledger, chaincode application(s) and the ordering service node(s).

<b>Chaincode </b> Chaincode is what Ethereum calls <b>Smart Contracts </b>. They are invoked by a client application external to the blockchain network – that manages access and modifications to a set of key-value pairs in the World State. Smart contract chaincode is installed onto peer nodes and instantiated to one or more channels.

<b>Peer</b> A network entity that hosts the ledger and runs chaincode containers in order to perform read/write operations to the ledger. Peers are owned and maintained by members.

<b>Hyperledger Fabric CA </b> is the default Certificate Authority component, which issues PKI-based certificates to network member organizations and their users. The CA issues one root certificate (rootCert) to each 

<b>Orderer</b> is responsible for establishing consensus. It is a defined collective of nodes that orders transactions into a block. The ordering service exists independent of the peer processes and orders transactions on a first-come-first-serve basis for all channel’s on the network. The ordering service is designed to support pluggable implementations beyond the out-of-the-box SOLO and Kafka varieties. The ordering service is a common binding for the overall network; it contains the cryptographic identity material tied to each Member.

<b>Consensus</b> is the process of reaching agreement on the next set of transactions to be added to the ledger. First a transaction must be endorsed, then passed to the Orderers for validation and commitment.

## Exercise 0: Blockchain Platform Playground: https://blockchaindevelop.mybluemix.net/login
## Exercise 1: First Steps Building Hyperledger Applications [Start bulding Hyperledger Fabric applications](HL%20BYFA.md)
## Exercise 2: Decentralized Energy Composer: https://github.com/IBM/Decentralized-Energy-Composer 
## Demo: [The Blockchain Bean](https://www.ibm.com/thought-leadership/blockchainbean/)
## Exercise 3: [The Marbles App](https://github.com/IBM-Blockchain/marbles)
## Exercise 4: IBM Blockchain Platform

<img src="https://github.com/LennartFr/hyperlab20181018/blob/master/IBM%20Cloud%20Samples.png">

https://www.ibm.com/blockchain/platform?|1298|22081

https://github.com/IBM-Blockchain/vehicle-manufacture. Click on Blue Button to kick off the deployment.


<img src="https://github.com/LennartFr/hyperlab20181018/blob/master/car.png">


https://vehicle-manufacture-basilar-fenestration.mybluemix.net/tutorial

<img src="https://github.com/LennartFr/hyperlab20181018/blob/master/ibmcloudbc-1.png">

# Where do we go from here?

1. Go through the IBM Code Patterns for Blockchain. https://developer.ibm.com/patterns/category/blockchain/
1. Create more advanced applications from the list of IBM Use Cases 
1. Engage with IBM Developer Advocates on your plans and ISV free resources
1. https://www.coindesk.com/ibm-wants-know-ways-blockchain-can-go-wrong/

# Appendix
