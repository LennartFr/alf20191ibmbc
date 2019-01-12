
<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Fabcar, writing your first application on the Hyperledger Fabric network

[Read the docs: Writing your first application: ](https://hyperledger-fabric.readthedocs.io/en/release-1.4/write_first_app.html#writing-your-first-application)

If you haven't gone thru the [Build your first network portion of this workshop](https://github.com/LennartFr/alf20191ibmbc/blob/master/HL%20BYFA.md#build-your-first-hyperedger-fabric-network), you need to start by pulling down the docker images with curl:

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
