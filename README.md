# Block_Party

![](https://i0.wp.com/dailyhodl.com/wp-content/uploads/2019/09/crypto-party.jpg?fit=810%2C475&ssl=1)


A step by step guide to setting up blockchain testnet using local network. This example is presented on macOS.


## Necessary Installations:
* Install MyCrypto https://download.mycrypto.com/ (macOS may need to adjust permissions to open apps from unidentified developers:  >> System Preferences >> Security & Privacy). For this tow work, you will need to generate 2 new wallets and store address and private key in a secure location. Use your preferred method of authentication (mneumonic, keystore, etc). **DO NOT SHARE YOUR PRIVATE KEY with anyone, under any circumstances.**
* Install Go Ethereum Tools https://geth.ethereum.org/downloads/. Be sure to download the latest stable release bundle for your operating system. Decompress archive into local repo where you plan to run your nodes. For this example, we will be using a repo called 'Block_Party'.

## Creating a Genesis network
Open terminal / git bash and navigate to newly created Block_Party repo. Proceed with the
following commands:

1. Initialize Puppeth blockchain service management tool:
./puppeth 

2. You will be prompted to specify a network name. In this example, we will use 'party'

3. In the prompt that follows, first select option '2' to configure a new genesis, then '1' to
create a new genesis from scratch and then '2' to select 'Proof-of-Authority' consensus engine. DEFAULT options for how long block should take

4. When prompted, paste both wallet addresses one at a time into the list of accounts to seal. (note: first 2 alphanumerics '0x' provided)

5. Paste the wallet addresses again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund. Choose 'no' when prompted to pre-fund with wei as it keeps genesis cleaner

6. Specify network/chain ID as '42069'

7. Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option. 

8. Export genesis configurations. This will fail to create two of the files, but you only need party.json file. You can delete the party-harmony.json file from the repo.

9. Use the control + c command on keyboard to exit from puppeth

10. Create directory for 1st node within the Block_Party repo
./geth account new --datadir n1

After entering this line of code, you will be prompted to provide a password. Once provided, 
you will see a public address for the new key as well as the filepath to the secret key file in the terminal. Be sure to save all of this information as it will be needed later. 

11. Create directory for 2nd node
./geth account new --datadir n2

12. Initialize each node with the new party.json with geth.
./geth --datadir n1 init party.json
./geth --datadir n2 init party.json

13. Run the first node, unlock the account, enable mining, and the RPC flag. Only one node needs RPC enabled.
./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
** Be sure to copy down the enode address as it will be needed in the next step. This address 
appears after 'Starting P2P Networking' appears in Terminal

14. Open a new terminal and navigate to Block_Party repo. Start second node 
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock

NOTE: Type your password and hit enter - even if you can't see it visually!
Your private PoA blockchain should now be running!

With both nodes up and running, the blockchain can be added to MyCrypto for testing.


## Send Test Transaction
### Use the MyCrypto GUI wallet to connect to the node with the exposed RPC port. 

1. Open the MyCrypto app, then click Change Network at the bottom left:

![]

2. Click "Add Custom Node", then add the custom network information that you set in the genesis.

3. Make sure that you scroll down to choose Custom in the "Network" column to reveal more options like Chain ID. You will need to select the custom network that was just created and input the chain ID '42069'. Use ETH as currency and local host network: http://127.0.0.1:8545 (This points to the default RPC port on your local machine). Once all fields have been addressed, click [Save & Use Custom Node]

![]


4. After connecting to the custom network in MyCrypto, it can be tested by sending money between accounts.



3. Copy the transaction hash and paste it into the "TX Status" section of the app, or click "TX Status" in the popup.







