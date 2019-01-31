<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Commercial Paper Tutorial 

[By Paul O'Mahony  Published December 11, 2018 - Updated December 11, 2018](https://developer.ibm.com/tutorials/run-commercial-paper-smart-contract-with-ibm-blockchain-vscode-extension/)

## [Commercial Paper Tutorial source](https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html#commercial-paper-tutorial)

## Step 0 [Pre-requisites](https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html#prerequisites)

~~~~
docker rm -f $(docker ps -aq)

docker network prune ; docker volume prune

docker network prune ; docker volume prune

~~~~

## Step 1 Get the Commercial Paper sample

~~~~

git clone https://github.com/hyperledger/fabric-samples

~~~~

## Step 2 Explore the papercontract.js file, which is located in the lib subfolder. 
It effectively orchestrates the logic for the different smart contract transaction functions (issue, buy, redeem, etc.), and is underpinned by essential core functions (in the sample contract) that interact with the ledger. The link provided in the introduction section above explains the concepts, themes, and programmatic approach to writing contracts using the commercial paper scenario. Take some time to read that explainer and then resume here.

## Step 3 Open the commercial paper contract 

### Step 3.1 In VSCode, choose File > Open Folder, 
and select the contracts folder by navigating to the $HOME/fabric-samples/commercial-paper/organization/magnetocorp directory. This is your top-level project folder for this tutorial.
Click on the Explorer icon (top left) and open the contract folder under $HOME/fabric-samples/commercial-paper/organization/magnetocorp/.

### Step 3.2 Click on the Explorer icon (top left) 
and open the contract folder under $HOME/fabric-samples/commercial-paper/organization/magnetocorp/.

### Step 3.3 Explore the papercontract.js file, 
which is located in the lib subfolder. It effectively orchestrates the logic for the different smart contract transaction functions (issue, buy, redeem, etc.), and is underpinned by essential core functions (in the sample contract) that interact with the ledger. The link provided in the introduction section above explains the concepts, themes, and programmatic approach to writing contracts using the commercial paper scenario. Take some time to read that explainer and then resume here.

### Step 3.4 Go back to the contract folder 
by clicking on the folder name on the left in the VSCode Explorer. It’s important to do so before the next step.

## Step 4. Package the smart contract

### Step 4.1 
Click on the package.json file in the Explorer palette and edit the “name” field; change the name to papercontract.

### Step 4.2 
Edit these existing “dependencies” entries (as necessary). They should read as follows:
~~~~
"fabric-contract-api": "~1.4.0",

 "fabric-shim": "~1.4.0"
~~~~

Now save (CTRL + S) the file

### Step 4.3

Click on the IBM Blockchain Platform sidebar icon. When you do this the first time, you may get a message that the extension is “activating” in the output pane.

### Step 4.4

Click on the “+” symbol (“Add a new package”), under the ‘Smart Contract packages’ panel, to package up the commercial paper smart contract package for installing onto a peer. It will be called something like papercontract@0.0.1.

## Step 5 Install the smart contract on a running Fabric

### Step 5.1

Let’s start up a sample Fabric runtime environment from the downloaded Hyperledger Fabric samples to run the smart contract. To that end, we’ve provided a sample connection.json to import into the IBM Blockchain VSCode environment; the beauty here is that you can connect to the local Fabric provided, or to one you’ve already got up and running. The Fabric sample uses its own “basic-network” sample. In a terminal window copy the following command sequence:
cd $HOME/fabric-samples/basic-network
./start.sh
Wait for the output message to indicate that the Fabric network has been started (message: “Successfully submitted proposal to join channel”).

### Step 5.2

You’ll also need to download the following commpaper sample Github repository (“repo”) as it has tutorial artifacts, including the connection profile for the VSCode extension that’s used to connect to the blockchain network. You’ll import it using the IBM Blockchain Platform VSCode extension (as well an admin certificate in the same repo that you’ll use in the demo):
cd $HOME
git clone https://github.com/mahoney1/commpaper

### Step 5.3
Back in VSCode, click on the “IBM Blockchain Platform” sidebar icon in VSCode (at the bottom left). You’ll see an “IBM Blockchain Connections” sidebar panel.
### Step 5.4
Next, collapse the Smart Contract Packages using the twisty and expand the Blockchain Connections panel.
### Step 5.5
Click the Add New Connection button or icon. Enter “myfabric” for the connection name and then browse to find and import the connection.json file from the commpaper repo that you cloned earlier.

### Step 5.6
Next, browse and select the AdminCert for the certificate file to import and “browse … select” the Adminkey for the key file.

### Step 5.7
You should now be able to click on myfabric and see the channel mychannel become active. Click mychannel to drill down and see the only peer in the basic-network network.

### Step 5.8
Right-click on the peer node, peer0.org1.example.com, and elect to Install Smart Contract. Then choose the papercontract@0.0.1 package from the list up top.
### Step 5.9
Next, highlight the channel mychannel and right-click and choose to Instantiate Smart Contract; select papercontract as the contract to instantiate.

### Step 5.10
Paste in the string org.papernet.commercialpaper:instantiate when prompted to enter a function name to call, and hit ENTER.

### Step 5.11
When you’re prompted to enter arguments, hit ENTER to leave it blank (there are no arguments in this case). After a minute or so, you should see a progress message in the output pane.
1







<img src="https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/commercial_paper.diagram.1.png">

~~~~
0. Run a commercial paper smart contract with the IBM Blockchain VSCode extension: https://developer.ibm.com/tutorials/run-commercial-paper-smart-contract-with-ibm-blockchain-vscode-extension/

1. Commercial Paper Tutorial https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html

2. Commercial Paper Github Repo https://github.com/hyperledger/fabric-samples/tree/release-1.4/commercial-paper

3.Prerequisites https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html#prerequisites

4. Git clone Fabric samples:  git clone https://github.com/hyperledger/fabric-samples.git

5. Create Network: https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html#create-network

$ cd fabric-samples/basic-network
$ ./start.sh


Creating network "net_basic" with the default driver
Creating ca.example.com      ... done   //Certificate authority
Creating orderer.example.com ... done
Creating couchdb             ... done
Creating peer0.org1.example.com ... done


~~~~

Setup GOPATH on the MAC:

~~~~

echo $SHELL

Edit ~/.bash_profile
export GOPATH+$HOME/go
save and exit editor
source ~/.bash_profile

Open a new terminal window and check your $GOPATH is set using the env command:

~~~~

 
