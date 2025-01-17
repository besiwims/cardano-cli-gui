# cardano-cli-gui
Simple GUI that cover some basic functionality of the 
[Cardano CLI](https://github.com/input-output-hk/cardano-cli) 
command line tool.

**WARNING:** <br/>
**The GUI was created for educational purposes and is not regularly updated with changes in the Cardano CLI. If you want to use the GUI for submitting transactions on the main net you are doing so at your own risk.**

To run the GUI you can use the executable files in the `executables/` folder. Download 
the executable for your OS. If you want to use the GUI also in debug mode you should run 
the executable from a terminal window. Then in debug mode the GUI prints the cardano-cli 
commands to the terminal window instead of acctually executing them. 

You can also run the GUI from source. In that case you need to have `python 3` and `PyQt 5` 
installed for the GUI to work. Simply download this repository, open a terminal in the 
downloaded folder and run:
```console
python cardano-cli-gui.py
```

**IMPORTANT: To use the *query* and *send* command in the GUI a cardano node has to be running and synced to the test or main network.**

To run a cardano node download it from [here](https://github.com/input-output-hk/cardano-node/releases) and install it. The installer files are located under the Assets section that needs to be expanded. Add all executable files including the `cardano-node` and `cardano-cli` to you system path, e.g. copy them to `/usr/local/bin/`. 

Then download the configurations files for the Preview testnet from [here](https://book.world.dev.cardano.org/environments.html#preview-testnet) or for the Preprod testnet from [here](https://book.world.dev.cardano.org/environments.html#pre-production-testnet). 

From the folder that contains your configuration files run: 
```console
cardano-node run \
 --topology topology.json \
 --database-path db \
 --socket-path node.socket \
 --host-addr 0.0.0.0 \
 --port 3001 \
 --config config.json
```

The `node.socket` file will be created in the folder from where you ran the above command. 
Stop the node and add to the end of your *.bashrc* file that is located in your HOME folder the follwoing line:
```console
export CARDANO_NODE_SOCKET_PATH="$HOME/<path>/<to>/node.socket"
```
Source the *.bashrc* file:
```console
source ~/.bash.rc
```
Start the cardano node again. You can check how much the node is synced if you go to the **Query** tab of the GUI. 
There select mainnet or testnet and press the *Query info* button. If you then scroll down in the text box you will see the field *syncProgress*. 

You can also check the sync progress for the testnet with the following command: 
```console
cardano-cli query tip --testnet-magic <testnet_number> 
```
For the testnet number use 1 for preprod and 2 for preview. 

GUI design
----------

The GUI functionality is seperated in 7 tabs and covers following things:

1. **Start** tab, that notifies the user that he has to set a valid folder path to unlock
other tabs. The folder path will be used to load and save key and address files. It also
displays if the *Debug mode* is set ON or OFF.

![alt text](https://github.com/LukaKurnjek/cardano-cli-gui/blob/main/images/start.png) 

2. **Wallet** tab, that handles loading or generating verification and signing keys, 
payment addresses and payment public key hashes.  

![alt text](https://github.com/LukaKurnjek/cardano-cli-gui/blob/main/images/wallet.png)

3. **Transactions** tab, that handles checking funds for a payment address and sending 
funds to a receiving address.

![alt text](https://github.com/LukaKurnjek/cardano-cli-gui/blob/main/images/transactions.png)

4. **Smart contracts - send** tab, that handles building a script payment address for a script 
file. You can also send funds to the generated script address and attach a datum to the transaction. 

![alt text](https://github.com/LukaKurnjek/cardano-cli-gui/blob/main/images/smart_contracts_send.png)

5. **Smart contracts - receive** tab, that handles creating a spending transactions that spends a 
script address UTxO You can attach a datum and a redeemer to the transaction and set a validity interval.

![alt text](https://github.com/LukaKurnjek/cardano-cli-gui/blob/main/images/smart_contracts_receive.png)

6. **Query** tab, that lets you query an address for funds, query net information and generate
the protocol parameters file for the chosen net. 

![alt text](https://github.com/LukaKurnjek/cardano-cli-gui/blob/main/images/query.png)

7. **Developer** tab, that lets more experienced users set a different testnet 
magic number or update the era parameter. 

![alt text](https://github.com/LukaKurnjek/cardano-cli-gui/blob/main/images/developer.png)
