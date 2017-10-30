Tor Support
=========

Rubycoin can be run as a hidden service.


## Ubuntu / Debian

* Installation

        sudo apt-get install tor

* Prepare folder

        mkdir /var/lib/tor/hidden_service
        chmod 700 /var/lib/tor/hidden_service
        chown debian-tor:debian-tor /var/lib/tor/hidden_service

* Edit /etc/tor/torrc

        DataDirectory /var/lib/tor
        HiddenServicePort 5937 127.0.0.1:5937
        HiddenServiceDir /var/lib/tor/hidden_service/

* Restart service

        service tor restart

* Get onion address (for the next step)

        cat /var/lib/tor/hidden_service/hostname

* Edit rubycoin.conf

        listen=1
        discover=1
        tor=127.0.0.1:9050
        externalip=o4aggcyknrekoce2.onion

* Restart rubycoind

        ./rubycoind stop
        ./rubycoind -daemon

* Confirm

        ./rubycoind getinfo
        "ip" : "o4aggcyknrekoce2.onion"

## Privacy

When **externalip** is specified, no attempt is made to discover local IPv4 or IPv6 addresses. If you want to run a dual setup, reachable from both Tor and the clearnet, you will need to either pass your other addresses using **externalip**, or enable **discover**. All addresses of a dual setup may be easily linkable using traffic analysis.