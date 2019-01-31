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

git clone https://github.com/hyperledger/fabric-samples


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


