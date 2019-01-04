
<img src="/Screen Shot 2018-12-30 at 08.48.23.png">

## Your first steps on the way to building Hyperledger Fabric applications

Hyperledger Fabric comes with the excellent <a href="https://hyperledger.github.io/composer/latest/installing/installing-index.html">Hyperledger Composer tool </a> that makes easy to quickly come up to speed writing Fabric applications.

But the Composer will not have the same central role in the Hyperledger Fabric architecture that it had in 2018. Which leades to the question of how you create your very first Hyperledger Fabric app outside of the warm confines of Composer?

Let's take a look at an alternative way of getting started by leveraging two Hyperledger Sample apps on the Hyperledger  <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.3/build_network.html">ReadTheDocs site.</a>

The first is <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.3/build_network.html">Build Your First Network </a> with the BYFN.sh script.

The second is the <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.3/write_first_app.html?highlight=fabcar#writing-your-first-application">Writing your first Application</a> commonly known as FabCar.

And the third application is the <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html#commercial-paper-tutorial">Commercial paper tutorial</a> for Hyperledger Release 1.4.

So let's get started with build your first network.

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

## Step 1: Make sure you have the right pre-reqs.

So let's start with <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.3/prereqs.html#prerequisites"> the pre-reqs</a> 

## Step 2 Download the Docker images of the Fabric code from GitHub

We will also need to install <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.3/install.html#install-samples-binaries-and-docker-images">Binaries and Docker Images with curl</a>, see line below:

~~~~
curl -sSL http://bit.ly/2ysbOFE | bash -s 1.3.0  
~~~~
creates the directory fabric-samples and pulls down the following docker images:

~~~~
1. hyperledger/fabric-ca   https://hyperledger-fabric-ca.readthedocs.io/en/latest/users-guide.html#fabric-ca-user-s-guide
1. hyperledger/fabric-zookeeper  https://hyperledger-fabric.readthedocs.io/en/release-1.3/kafka.html#bringing-up-a-kafka-based-ordering-service
1. hyperledger/fabric-kafka https://hyperledger-fabric.readthedocs.io/en/release-1.3/kafka.html#bringing-up-a-kafka-based-ordering-service1. hyperledger/fabric-couchdb
1. hyperledger/fabric-javaenv
1. hyperledger/fabric-tools
1. hyperledger/fabric-ccenv
1. hyperledger/fabric-orderer  https://hyperledger-fabric.readthedocs.io/en/release-1.1/ordering-service-faq.html#ordering-service-faq
1. hyperledger/fabric-peer  https://hyperledger-fabric.readthedocs.io/en/release-1.3/peers/peers.html#peers
~~~~

Hyperledger is advancing quite quickly so the version number may well have changed by the time you see this article.
The download will take a minute or two. The download will install a directory called fabric-samples. Take time to familiarize yourself with the Hyperledger docker images that you have downloaded.

## Step 3 Let's build our first network with the byfn.sh script.

We are now ready to build our first network. We do this by 

~~~~
cd /fabric-samples/first-network.
~~~~

Here we find the <b>byfn.sh </b> script. This Swiss Army knife type of script leverages the Docker images we have just downloaded to "quickly bootstrap a Hyperledger Fabric network comprised of 4 peers representing two different organizations, and an orderer node. It will also launch a container to run a scripted execution that will join peers to a channel, deploy and instantiate chaincode and drive execution of transactions against the deployed chaincode."

~~~~
./byfn.sh generate

and here is the output from the script

1. generate certificates using cryptogen tool
2. generate Orderer Genesis Block
3. Generate channel configuration transaction 'channel.txt'
4. Generate anchor peer update for Org1MSP
5. Generate anchor peer update for Org2MSP
~~~~

Followed by running <b>byfn.sh up</b> which brings up the Hyperledger artefacts on your laptop. Please check out the voluminous script output.

~~~~

===================== Invoke transaction successful on peer0.org1 peer0.org2 on channel 'mychannel' ===================== 

Installing chaincode on peer1.org2...
+ peer chaincode install -n mycc -v 1.0 -l golang -p github.com/chaincode/chaincode_example02/go/
+ res=0
+ set +x
2019-01-03 22:29:59.618 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
2019-01-03 22:29:59.619 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
2019-01-03 22:29:59.932 UTC [chaincodeCmd] install -> INFO 003 Installed remotely response:<status:200 payload:"OK" > 
===================== Chaincode is installed on peer1.org2 ===================== 

Querying chaincode on peer0.org1...
===================== Querying on peer0.org1 on channel 'mychannel'... ===================== 
Attempting to Query peer0.org1 ...3 secs
+ peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
+ res=0
+ set +x

100

Querying chaincode on peer1.org2...
===================== Querying on peer1.org2 on channel 'mychannel'... ===================== 
+ peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
Attempting to Query peer1.org2 ...3 secs
+ res=0
+ set +x

90
~~~~

Followed by running ./byfn.sh down, to bring down the network.

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Fabcar, your first application running on Hyperledger Fabric

If you haven't gone thru the Build your first network portion of this workshop, you need to pull down the docker images with 

~~~~
curl -sSL http://bit.ly/2ysbOFE | bash -s 1.3.0
~~~~

## Step 1 Bring up and query the Fabric

We cd to fabric-samples/fabcar

~~~~ 
1. We begin by invoking: nvm use node
   Output on my laptop: Now using Node v8.11.2 (npm v6.4.1) 
2. We kill stale containers: docker rm -f $(docker ps -aq) 
3. and clear cached networks: docker network prune
4. and docker rmi dev-peer0.org1.example.com-fabcar-1.0-5c906e402ed29f20260ae42283216aa75549c571e2e380f3615826365d8269ba
5. In the fabcar directory we invoke the startFabric.sh script.
   The startFabric.sh script generates the following Fabric components:  
      Creating network "net_basic" with the default driver
      Creating orderer.example.com ... done
      Creating ca.example.com         ... done
      Creating couchdb             ... done
      Creating peer0.org1.example.com ... done
   The end of the startFabric.sh script instructs us to run the following commands:
6. npm install. If error: npm rebuild followed by startFabric.sh
7. node enrollAdmin.js
8. node registerUser.js
9. node query.js
~~~~




<img src="https://farm5.staticflickr.com/4525/26498674439_24631680fc_c.jpg" width="800" height="299" alt="Hyperledger helloworld">


Which will give us the output:

~~~~
Response is [{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},{"Key":"CAR1", "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},{"Key":"CAR2", "Record":{"colour":"green","make":"Hyundai","model":"Tucson","owner":"Jin Soo"}},{"Key":"CAR3", "Record":{"colour":"yellow","make":"Volkswagen","model":"Passat","owner":"Max"}},{"Key":"CAR4", "Record":{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}},{"Key":"CAR5", "Record":{"colour":"purple","make":"Peugeot","model":"205","owner":"Michel"}},{"Key":"CAR6", "Record":{"colour":"white","make":"Chery","model":"S22L","owner":"Aarav"}},{"Key":"CAR7", "Record":{"colour":"violet","make":"Fiat","model":"Punto","owner":"Pari"}},{"Key":"CAR8", "Record":{"colour":"indigo","make":"Tata","model":"Nano","owner":"Valeria"}},{"Key":"CAR9", "Record":{"colour":"brown","make":"Holden","model":"Barina","owner":"Shotaro"}}]
~~~~

