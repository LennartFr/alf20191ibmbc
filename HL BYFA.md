
# Your first steps on the way to building Hyperledger Fabric applications

Hyperledger Fabric comes with the excellent Hyperledger Composer tool that makes easy to quickly come up to speed writing Fabric applications.

But how do you create your very first Hyperledger Fabric app outside of the warm confines of Composer? Let's take a look at the Hyperledger sample app on the ReadTheDocs site. It is a simple car application that goes under the name of Fabcar, for "Fabric Car". The app allows us to add and delete cars and their owners from a common ledger. A good starting app that can easily be expanded in many directions.

So let's start with the pre-reqs. There are a fair number of pre-reqs and we need to take our time to make certain that we have them all.


https://hyperledger-fabric.readthedocs.io/en/release-1.3/install.html#install-samples-binaries-and-docker-images

# Step 2 Download the Docker images of the Fabric code from GitHub

With the pre-reqs in place we are ready to download the Hyperledger Fabric code: curl -sSL http://bit.ly/2ysbOFE | bash -s 1.3.0

curl -sSL http://bit.ly/2ysbOFE | bash -s 1.3.0  creates directory fabric-samples

hyperledger/fabric-ca
hyperledger/fabric-zookeeper
hyperledger/fabric-kafka
hyperledger/fabric-couchdb
hyperledger/fabric-javaenv
hyperledger/fabric-tools
hyperledger/fabric-ccenv
hyperledger/fabric-orderer
hyperledger/fabric-peer

Hyperledger is advancing quite quickly so the version number may well have changed by the time you see this article.
The download will take a minute or two. The download will install a directory called fabric-samples. Take time to familiarize yourself with the Hyperledger docker images that you have downloaded.


---

We are now ready to build our first network. We do this by cd into the fabric-samples directory and from there into the first-network directory.
Here we find the byfn.sh script. This Swiss Army knife type of script leverages the Docker images we have just downloaded to "quickly bootstrap a Hyperledger Fabric network comprised of 4 peers representing two different organizations, and an orderer node. It will also launch a container to run a scripted execution that will join peers to a channel, deploy and instantiate chaincode and drive execution of transactions against the deployed chaincode."
Let's run this script: ./byfn.sh generate. Take a look at the output from the script to see what it is doing.
generate certificates using cryptogen tool
generate Orderer Genesis Block
Generate channel configuration transaction 'channel.txt'
Generate anchor peer update for Org1MSP
Generate anchor peer update for Org2MSP

Querying chaincode on peer0.org1…
Querying on peer0.org1 on channel 'mychannel'… 
Attempting to Query peer0.org1 …3 secs
+ peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
+ res=0
+ set +x
100
Followed by byfn.sh up which brings up the Hyperledger artefacts on your laptop. Please check out the voluminous script output.
create mychannel
having all peers join the channel
peer channel join -b mychannel.block. Endorser and orderer connections initialized



Follow the execution of the script.
Followed by ./byfn.sh down 


---

Step 4 Bringing up and query the Fabric
We then do cd to fabric-samples/fabcar
we kill stale containers: docker rm -f $(docker ps -aq)
and clear cached networks: docker network prune
docker rmi dev-peer0.org1.example.com-fabcar-1.0-5c906e402ed29f20260ae42283216aa75549c571e2e380f3615826365d8269ba
In the fabcar directory we invoke the startFabric.sh script.

The end of the startFabric.sh script instructs us to run the following commands:
2. npm install. If error: npm rebuild followed by startFabric.sh
3. node enrollAdmin.js
4. node registerUser.js
5 node query.js
Which will give us the output:
Response is [{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},{"Key":"CAR1", "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},{"Key":"CAR2", "Record":{"colour":"green","make":"Hyundai","model":"Tucson","owner":"Jin Soo"}},{"Key":"CAR3", "Record":{"colour":"yellow","make":"Volkswagen","model":"Passat","owner":"Max"}},{"Key":"CAR4", "Record":{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}},{"Key":"CAR5", "Record":{"colour":"purple","make":"Peugeot","model":"205","owner":"Michel"}},{"Key":"CAR6", "Record":{"colour":"white","make":"Chery","model":"S22L","owner":"Aarav"}},{"Key":"CAR7", "Record":{"colour":"violet","make":"Fiat","model":"Punto","owner":"Pari"}},{"Key":"CAR8", "Record":{"colour":"indigo","make":"Tata","model":"Nano","owner":"Valeria"}},{"Key":"CAR9", "Record":{"colour":"brown","make":"Holden","model":"Barina","owner":"Shotaro"}}]



docker rm $(docker ps -aq) // Raheel

docker rmi $(docker images dev-* -q) // Rhaheel

