# MN-Install

Explanation of how to activate MasterStake MN

Install a masternode for your coin on Ubuntu Server 18.04 with the following tutorial.

Open your Windows wallet.

Go to Tools -> Debug console.

Type the following RPC command, to create private key for your masternode:

createmasternodekey

Example output

75eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo

Type the following RPC command, to create an address for the masternode amount fee:

getaccountaddress "MN1"

Example output

TRPLV4dXmEFMSgXg2Xu6skN9pmw8TAo4N5

Go back to your wallet overview

Press on the toolbar button "Send".

Enter the address from the RPC command “getaccountaddress "MN1"” behind the text "Pay To:". (Example: TRPLV4dXmEFMSgXg2Xu6skN9pmw8TAo4N5)

Enter the following amount of coins behind the text "Amount:": 1000

Press on the button "Send".

Wait until the transaction is confirmed by 11 blocks.

Go back to the console of your wallet.

Identify the transaction with the following RPC command:

getmasternodeoutputs

Example output

{
 "fdab9dff1ff9caf5d291905ad43b9f7d69775189d4d22cb085d7fedd94ea1c6a": "0"
}

Go to Tools -> Open Masternode Configuration File.

Paste the following text into notepad.

MN1 203.0.113.53:49266 75eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo 06e38868bb8f9958e34d5155437d009b72dff33fc28874c87fd42e51c0f74fdb 0

MN1 - Alias for your masternode.

203.0.113.53 - External IPv4 address of your VPS.

75eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo - Private masternode key from the RPC command “createmasternodekey”.

06e38868bb8f9958e34d5155437d009b72dff33fc28874c87fd42e51c0f74fdb - Transaction hash from the RPC command “getmasternodeoutputs”.

0 - Single digit from the RPC command “masternode outputs”.

Save and close notepad.

Close your wallet.

Open putty and connect using SSH with your Ubuntu 18.04 server.

Update your Ubuntu server with the following command:

sudo apt-get update && sudo apt-get upgrade -y

Install the required dependencies with the following command:

sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils python3 libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-test-dev libboost-thread-dev libboost-all-dev libboost-program-options-dev libminiupnpc-dev libzmq3-dev libprotobuf-dev protobuf-compiler unzip software-properties-common cmake -y

Install the repository ppa:bitcoin/bitcoin with the following command:

sudo add-apt-repository ppa:bitcoin/bitcoin

Confirm the installation of the repository by pressing on the enter key. enter

Install Berkeley DB with the following command:

sudo apt-get update && sudo apt-get install libdb4.8-dev libdb4.8++-dev -y

Download the Linux daemon for your wallet with the following command:

wget "https://github.com/carlinhos2008/Master-2.0.1/releases/download/2.0.1/MASTER-Ubuntu1804.zip" -O MASTER-Ubuntu1804.zip

Extract the tar file with the following command:

unzip MASTER-Ubuntu1804.zip

Type the following command to install the daemon and tools for your wallet:

sudo mv masterstaked masterstake-cli masterstake-tx /usr/bin/

Create the data directory for your coin with the following command:

mkdir $HOME/.masterstake

Open nano.

nano $HOME/.masterstake/masterstake.conf -t

Paste the following into nano.

rpcuser=rpc_masterstake
rpcpassword=dR2oBQ3K1zYMZQtJFZeAerhWxaJ5Lqeq9J2
rpcallowip=127.0.0.1
listen=1
server=1
daemon=1
maxconnections=100
masternode=1
masternodeprivkey=0acbf6f183d0c9b794b9bc0dba25f8a1a1eca21aa4f2e4a86ecd3120a59efb35
addnode=84.54.23.196
addnode=164.68.123.250
addnode=167.86.80.59
addnode=45.94.209.55

203.0.113.53 - External IPv4 address of your VPS.

0acbf6f183d0c9b794b9bc0dba25f8a1a1eca21aa4f2e4a86ecd3120a59efb35 - Private masternode key from the RPC command “createmasternodekey”.

Save the file with the keyboard shortcut ctrl + x.

Type the following command to start your daemon:

masterstaked

Open your Windows wallet.

Go to Tools -> Debug console.

Type the following RPC command, to start your masternode:

startmasternode alias false MN1

