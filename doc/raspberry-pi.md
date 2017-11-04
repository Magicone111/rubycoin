Staking on a Raspberry Pi
===================================

The Raspberry Pi is a series of small single-board computers intended to promote the teaching of basic computer science in schools and in developing countries. Rubycoin can stake on these devices.

## Raspbian

* Increase swap memory

        sudo sed -i 's/CONF_SWAPSIZE=100/CONF_SWAPSIZE=1024/g' /etc/dphys-swapfile

* Restart service

        $ sudo /etc/init.d/dphys-swapfile stop
        $ sudo /etc/init.d/dphys-swapfile start

* Edit source

        $ sudo sed -i 's/jessie/stretch/g' /etc/apt/sources.list
        $ sudo apt update

* Install dependencies

        $ sudo apt install git build-essential libssl-dev libdb++-dev libboost-all-dev make

* Set timezone and locale under localization options

        $ sudo raspi-config

* Install Rubycoin

        $ git clone https://github.com/rubycoinorg/rubycoin
        $ cd rubycoin/src
        $ make -f makefile.unix

* Edit config

        $ sh -c "echo 'rpcuser=YOUR_RPC_USERNAME\nrpcpassword=YOUR_RPC_PASSWORD'" >> ~/.rubycoin_v2.conf

* Start rubycoind

        $ ./rubycoind -daemon

* Verify syncing

        $ ./rubycoind getinfo
            "blocks" : 12345,
            "connections" : 8,
     

* Encrypt wallet

        $ ./rubycoind encryptwallet YOUR_SUPER_SECURE_PASSWORD

* Decrypt for staking only

        $ ./rubycoind walletpassphrase YOUR_SUPER_SECURE_PASSWORD 31557600 true

* Get an address to fund for staking

        $ ./rubycoind getnewaddress

## Swap memory

After compiling, swap memory should be decreased back to the default value.

* Decrease swap memory

        sudo sed -i 's/CONF_SWAPSIZE=1024/CONF_SWAPSIZE=100/g' /etc/dphys-swapfile

* Restart service

        $ sudo /etc/init.d/dphys-swapfile stop
        $ sudo /etc/init.d/dphys-swapfile start

## External drive

Compile time can be improved by using an external drive.

* Mount drive

        $ mkdir ~/.rubycoin_v2
        $ sudo mount /dev/sdXY ~/.rubycoin_v2
