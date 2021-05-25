# Block_Party

![](https://i0.wp.com/dailyhodl.com/wp-content/uploads/2019/09/crypto-party.jpg?fit=810%2C475&ssl=1)


A step by step guide to setting up blockchain testnet using local network. This example is presented on Mac OSX


## Necessary Installations:
* Install MyCrypto https://download.mycrypto.com/ (Mac OS may need to adjust permissions to open apps from unidentified developers:  >> System Preferences >> Security & Privacy)
* Install Go Ethereum Tools https://geth.ethereum.org/downloads/. Be sure to download the latest stable release bundle for your operating system. Decompress archive into local repo where you plan to run your nodes. For this example, we will be using 'Block_Party'.

## Creating a Genesis network
Open terminal / git bash and navigate to newly created Block_Party repo. Proceed with the
following commands:

1. Initialize Puppeth blockchain service management tool:
./puppeth 

2. You will be prompted to specify a network name. In this example, we will use 'jorg'

3. In the prompt that follows, firth select option '2' to configure a new genesis, then '1' to
create a new genesis from scratch and then 1 again to select 'Proof-of-Work' consensus engine.
Do not enter wallet address to pre-fund any accounts when prompted.

4. Assign network/chain ID as '42069'

5. Use the control + c command on keyboard to exit from puppeth

5. Create directory for 1st node
./geth account new --datadir n1

After entering this line of code, you will be prompted to provide a password. Once provided, 
you will see a public address for the new key as well as the filepath to the secret key file in the terminal. Be sure to save all of this information as it will be needed later. 

6. Create directory for 2nd node
./geth account new --datadir n2

7. initialize node1 on network
./geth init jorg/jorg.json --datadir --datadir n1

8. Start first note
./geth --datadir n1 --mine --minerthreads 1
Be sure to copy down the enode address as it will be needed in the next step. THis address 
appears after 'Starting P2P Networking' appears in Terminal

9. Open a new terminal and Start second node
./geth --datadir n2 --port 30304 --rpc --bootnodes “[ENODE 1]”


Note: use the following commands if terminal is shut down to reinitialize network:
./geth --datadir n1 --unlock "[ADDRESS1]" --mine --miner.threads 1

./geth --datadir n2 --unlock "[ADDRESS2]" --port 30304 --rpc --bootnodes "[ENODE1]" --ipcdisable --allow-insecure-unlock

## Send Test Transaction
1. Use the MyCrypto GUI wallet to connect to the node with the exposed RPC port. In order to do
this, you will need to select the custom network that was just created. use ETH as currency and local host network: http://127.0.0.1:8545

2. Import the keystore file from the node1/keystore directory into MyCrypto. This will import the private key.

3. Copy the transaction hash and paste it into the "TX Status" section of the app, or click "TX Status" in the popup.







