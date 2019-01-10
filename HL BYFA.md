
<img src="/Screen Shot 2018-12-30 at 08.48.23.png">

## Your first steps on the way to building Hyperledger Fabric applications

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

## Step 1: Make sure you have the right pre-reqs.

So let's start with <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.4/prereqs.html#prerequisites"> the pre-reqs</a> 

## Step 2 Download the Docker images of the Fabric code from GitHub

We will also need to install <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.4/install.html#install-samples-binaries-and-docker-images">Binaries and Docker Images with curl</a>, see line below:

~~~~
curl -sSL http://bit.ly/2ysbOFE | bash -s 1.4.0  
~~~~

creates the directory fabric-samples and pulls down the following docker images:

~~~~

hyperledger/fabric-tools                                                                                             
hyperledger/fabric-ccenv                                                                                                 hyperledger/fabric-orderer                                                                            
hyperledger/fabric-peer                                                                                              
hyperledger/fabric-ca                                                                                                       hyperledger/fabric-javaenv                                                                               
hyperledger/fabric-zookeeper                                                                             
hyperledger/fabric-kafka                                                                                              
hyperledger/fabric-couchdb                                                                                            
hyperledger/fabric-baseimage                                                                                     
hyperledger/fabric-tools                                                                                                      
~~~~

Hyperledger is advancing quite quickly so the version number may well have changed by the time you see this article.
The download will take a minute or two. The download will install a directory called fabric-samples. Take time to familiarize yourself with the Hyperledger docker images that you have downloaded.

## Step 3 Let's build our first network with the byfn.sh script.

We are now ready to [build our first network](https://hyperledger-fabric.readthedocs.io/en/release-1.4/build_network.html) 

cd fabric-samples/first-network
./byfn.sh generate

Which does the following:

1. Generate certificates using cryptogen tool 
1. Generating Orderer Genesis block (The first block of the blockchain)
1. Generating channel configuration transaction 'channel.tx'
1. Generating anchor peer update for Org1MSP  (MSP = Member Service Provider)
1. Generating anchor peer update for Org2MSP 

Followed by running <b>./byfn.sh up -l node</b> which brings up the Hyperledger network on your laptop. 

~~~~

Build your first network (BYFN) end-to-end test
Channel name : mychannel
Creating channel...
Endorser and orderer connections initialized
===================== Channel 'mychannel' created ===================== 
Having all peers join the channel...
peer0.org1 joined channel 'mychannel'
peer1.org1 joined channel 'mychannel'
peer0.org2 joined channel 'mychannel'
peer1.org2 joined channel 'mychannel'
Anchor peers updated for org 'Org1MSP' on channel 'mychannel'
Anchor peers updated for org 'Org2MSP' on channel 'mychannel'
Chaincode is installed on peer0.org1
peer chaincode install -n mycc -v 1.0 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/
Chaincode is installed on peer0.org2 
Chaincode is instantiated on peer0.org2 on channel 'mychannel'
Querying on peer0.org1 on channel 'mychannel'...
Query successful on peer0.org1 on channel 'mychannel'
Invoke transaction successful on peer0.org1 peer0.org2 on channel 'mychannel'
Querying on peer1.org2 on channel 'mychannel'...
Query successful on peer1.org2 on channel 'mychannel' =
All GOOD, BYFN execution completed
~~~~

The chaincode used is /fabric-samples/chaincode/chaincode_example02/node

At the end of running the chaincode we do  ./byfn.sh down, to bring down the network.

~~~~

Stopping cli                    ... done
Stopping peer0.org1.example.com ... done
Stopping orderer.example.com    ... done
Stopping peer1.org1.example.com ... done
Stopping peer1.org2.example.com ... done
Stopping peer0.org2.example.com ... done
Removing orphan container "couchdb"
Removing orphan container "ca.example.com"
Removing cli                    ... done
Removing peer0.org1.example.com ... done
Removing orderer.example.com    ... done
Removing peer1.org1.example.com ... done
Removing peer1.org2.example.com ... done
Removing peer0.org2.example.com ... done
Removing network net_byfn

~~~~





<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Fabcar, your first application running on Hyperledger Fabric

[Write your first app](https://hyperledger-fabric.readthedocs.io/en/release-1.4/write_first_app.html)

If you haven't gone thru the Build your first network portion of this workshop, you need to pull down the docker images with 

~~~~
curl -sSL http://bit.ly/2ysbOFE | bash -s 1.4.0  
~~~~

## Step 1 Bring up and query the Fabric

We cd to fabric-samples/fabcar

~~~~

1. We begin by invoking: nvm use node
   Output on my laptop: Now using Node v8.11.2 (npm v6.4.1) 
2. We kill stale containers: docker rm -f $(docker ps -aq) 
3. and clear cached networks: docker network prune
4. and docker rmi dev-peer0.org1.example.com-fabcar-1.0-5c906e402ed29f20260ae42283216aa75549c571e2e380f3615826365d8269ba

5. In the fabcar directory we invoke:
   ./startFabric.sh javascript  
6. cd javascript
7. npm install
8. ls install to see what the directory contains
9. node enrollAdmin.js
10. node registerUser.js
11. node query.js

~~~~

<img src="https://farm5.staticflickr.com/4525/26498674439_24631680fc_c.jpg" width="800" height="299" alt="Hyperledger helloworld">


Which will give us the output:

~~~~
Response is [{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},{"Key":"CAR1", "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},{"Key":"CAR2", "Record":{"colour":"green","make":"Hyundai","model":"Tucson","owner":"Jin Soo"}},{"Key":"CAR3", "Record":{"colour":"yellow","make":"Volkswagen","model":"Passat","owner":"Max"}},{"Key":"CAR4", "Record":{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}},{"Key":"CAR5", "Record":{"colour":"purple","make":"Peugeot","model":"205","owner":"Michel"}},{"Key":"CAR6", "Record":{"colour":"white","make":"Chery","model":"S22L","owner":"Aarav"}},{"Key":"CAR7", "Record":{"colour":"violet","make":"Fiat","model":"Punto","owner":"Pari"}},{"Key":"CAR8", "Record":{"colour":"indigo","make":"Tata","model":"Nano","owner":"Valeria"}},{"Key":"CAR9", "Record":{"colour":"brown","make":"Holden","model":"Barina","owner":"Shotaro"}}]
~~~~

## Step 2 Add a new car to the Ledger query the Fabric

Edit invoke.js and add your own data on the await contract line as shown below

~~~~

// Create a new gateway for connecting to our peer node.
        const gateway = new Gateway();
        await gateway.connect(ccp, { wallet, identity: 'user1', discovery: { enabled: false } });

        // Get the network (channel) our contract is deployed to.
        const network = await gateway.getNetwork('mychannel');

        // Get the contract from the network.
        const contract = network.getContract('fabcar');

        // Submit the specified transaction.
        // createCar transaction - requires 5 argument, ex: ('createCar', 'CAR12', 'Honda', 'Accord', 'Black', 'Tom')
        // changeCarOwner transaction - requires 2 args , ex: ('changeCarOwner', 'CAR10', 'Dave')
  ---->  await contract.submitTransaction('createCar', 'CAR13', 'Trabant', '1000', 'Black', 'Lennart');
        console.log('Transaction has been submitted');

        // Disconnect from the gateway.
        await gateway.disconnect();

~~~~

save file
on commandline, enter node invoke.js

Notice new entry in Ledger
~~~~

 [{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},{"Key":"CAR1", "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},{"Key":"CAR12", "Record":{"colour":"Black","make":"Honda","model":"Accord","owner":"Tom"}},{"Key":"CAR13", "Record":{"colour":"Black","make":"Trabant","model":"1000","owner":"Lennart"}},{"Key":"CAR2", "Record":{"colour":"green","make":"Hyundai","model":"Tucson","owner":"Jin Soo"}},{"Key":"CAR3", "Record":{"colour":"yellow","make":"Volkswagen","model":"Passat","owner":"Max"}},{"Key":"CAR4", "Record":{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}},{"Key":"CAR5", "Record":{"colour":"purple","make":"Peugeot","model":"205","owner":"Michel"}},{"Key":"CAR6", "Record":{"colour":"white","make":"Chery","model":"S22L","owner":"Aarav"}},{"Key":"CAR7", "Record":{"colour":"violet","make":"Fiat","model":"Punto","owner":"Pari"}},{"Key":"CAR8", "Record":{"colour":"indigo","make":"Tata","model":"Nano","owner":"Valeria"}},{"Key":"CAR9", "Record":{"colour":"brown","make":"Holden","model":"Barina","owner":"Shotaro"}}]

~~~~

### Let's take a look at a ChainCode written in Node:

Let's cd to fabric-samples/chaincode/chaincode_example02/node:



<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Commercial Paper Tutorial

[Commercial Paper Tutorial](https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html)





