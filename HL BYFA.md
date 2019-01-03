
<img src="/Screen Shot 2018-12-30 at 08.48.23.png">

# Your first steps on the way to building Hyperledger Fabric applications

Hyperledger Fabric comes with the excellent <a href="https://hyperledger.github.io/composer/latest/installing/installing-index.html">Hyperledger Composer tool </a> that makes easy to quickly come up to speed writing Fabric applications.

But the Composer will not have the same central role in the Hyperledger Fabric architecture that it had in 2018. Which leades to the question of how you create your very first Hyperledger Fabric app outside of the warm confines of Composer?

Let's take a look at an alternative way of getting started by leveraging two Hyperledger Sample apps on the Hyperledger  <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.3/build_network.html">ReadTheDocs site.</a>

The first is <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.3/build_network.html">Build Your First Network </a> with the BYFN.sh script.

The second is the <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.3/write_first_app.html?highlight=fabcar#writing-your-first-application"Writing your first Application</a> commonly known as FabCar.

And the third application is the <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html#commercial-paper-tutorial">Commercial paper tutorial/a> for Hyperledger Release 1.4.

So let's get started with build your first network.

# Step 1: Make sure you have the right pre-reqs.

So let's start with the pre-reqs. There are a fair number of pre-reqs and we need to take our time to make certain that we have them all. https://hyperledger-fabric.readthedocs.io/en/release-1.3/prereqs.html#prerequisites

With the pre-reqs in place we are ready to download the Hyperledger Fabric code: 

# Step 2 Download the Docker images of the Fabric code from GitHub

We will also need to install <a href="https://hyperledger-fabric.readthedocs.io/en/release-1.3/install.html#install-samples-binaries-and-docker-images">Binaries and Docker Images</a>, with curl, see line below.

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

# Step 3 Let's build our first network with the byfn.sh scrip.

We are now ready to build our first network. We do this by cd into the fabric-samples directory and from there into the first-network directory.

Here we find the <b>byfn.sh </b> script. This Swiss Army knife type of script leverages the Docker images we have just downloaded to "quickly bootstrap a Hyperledger Fabric network comprised of 4 peers representing two different organizations, and an orderer node. It will also launch a container to run a scripted execution that will join peers to a channel, deploy and instantiate chaincode and drive execution of transactions against the deployed chaincode."

Let's run this script: <b>./byfn.sh generate</b>. Take a look at the output from the script to see what it is doing.

~~~~
1. generate certificates using cryptogen tool
2. generate Orderer Genesis Block
3. Generate channel configuration transaction 'channel.txt'
4. Generate anchor peer update for Org1MSP
5. Generate anchor peer update for Org2MSP
~~~~

Some of the output is as follows:

~~~~
1. Querying chaincode on peer0.org1…
2. Querying on peer0.org1 on channel 'mychannel'… 
3. Attempting to Query peer0.org1 …3 secs
4. + peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
5. + res=0
6. + set +x
7. 100
~~~~

Followed by byfn.sh up which brings up the Hyperledger artefacts on your laptop. Please check out the voluminous script output.

~~~~
1. create mychannel
2. having all peers join the channel
3. peer channel join -b mychannel.block. Endorser and orderer connections initialized
4. Follow the execution of the script.
5. Followed by ./byfn.sh down 
~~~~

# Step 4 Bringing up and query the Fabric

<img src="https://farm5.staticflickr.com/4525/26498674439_24631680fc_c.jpg" width="800" height="299" alt="Hyperledger helloworld">

~~~~
1. We then do cd to fabric-samples/fabcar
2. we kill stale containers: docker rm -f $(docker ps -aq) 
3. and clear cached networks: docker network prune
4. and docker rmi dev-peer0.org1.example.com-fabcar-1.0-5c906e402ed29f20260ae42283216aa75549c571e2e380f3615826365d8269ba
5. In the fabcar directory we invoke the startFabric.sh script.
   The end of the startFabric.sh script instructs us to run the following commands:
6. npm install. If error: npm rebuild followed by startFabric.sh
7. node enrollAdmin.js
8. node registerUser.js
9. node query.js
~~~~

<img src="https://farm5.staticflickr.com/4523/38243385192_3283c6031a_c.jpg" width="800" height="425" alt="Hyperledger helloworld 2">

Which will give us the output:

~~~~
Response is [{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},{"Key":"CAR1", "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},{"Key":"CAR2", "Record":{"colour":"green","make":"Hyundai","model":"Tucson","owner":"Jin Soo"}},{"Key":"CAR3", "Record":{"colour":"yellow","make":"Volkswagen","model":"Passat","owner":"Max"}},{"Key":"CAR4", "Record":{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}},{"Key":"CAR5", "Record":{"colour":"purple","make":"Peugeot","model":"205","owner":"Michel"}},{"Key":"CAR6", "Record":{"colour":"white","make":"Chery","model":"S22L","owner":"Aarav"}},{"Key":"CAR7", "Record":{"colour":"violet","make":"Fiat","model":"Punto","owner":"Pari"}},{"Key":"CAR8", "Record":{"colour":"indigo","make":"Tata","model":"Nano","owner":"Valeria"}},{"Key":"CAR9", "Record":{"colour":"brown","make":"Holden","model":"Barina","owner":"Shotaro"}}]
~~~~

# Step 5 Changing the Fabcar app to something else
