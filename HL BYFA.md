
https://hyperledger-fabric.readthedocs.io/en/release-1.3/install.html#install-samples-binaries-and-docker-images
curl -sSL http://bit.ly/2ysbOFE | bash -s 1.3.0  creates directory fabric-samples
The supplied commands in this documentation MUST be run from your first-network sub-directory of the fabric-samples repository clone

Run byfn.sh up in first-network

./startFabric.sh

./npm install

Start by installing required packages run 'npm install'

Then run 'node enrollAdmin.js', then 'node registerUser'

The 'node invoke.js' will fail until it has been updated with valid arguments

The 'node query.js' may be run at anytime once the user has been registered





# [Prerequisites](https://hyperledger-fabric.readthedocs.io/en/release-1.3/prereqs.html)
# [Building your first Network](https://hyperledger-fabric.readthedocs.io/en/release-1.3/build_network.html)
# [Install Sample, Binaries and Docker Images](https://hyperledger-fabric.readthedocs.io/en/release-1.3/install.html)
curl -sSL http://bit.ly/2ysbOFE | bash -s 1.3.0
# [Writing your first Application](https://hyperledger-fabric.readthedocs.io/en/release-1.3/write_first_app.html)

byfn.sh in fabric-samples/first-network/byfn.sh up  brings up network



startfabric.sh in /fabcar

nvm use node

docker kill $(docker ps -q) // Raheel

docker rm $(docker ps -aq) // Raheel

docker rmi $(docker images dev-* -q) // Rhaheel


