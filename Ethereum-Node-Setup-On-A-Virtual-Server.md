For setting up Ethereum nodes on the ETH and ETC chain using Ubuntu 16x LTS Linux services like Linode or Digital Ocean.

The blockchain data for the setup below is are `--fast` or `--warp` synced (currently < 15Gb), which is not a full archive node (currently about 140Gb). Once `--fast` or `--warp` synced, the blockchain data will grow at the same rate as a full archive node. This blockchain data will have to be removed and re `--fast` or `--warp` synced periodically to keep the disk space requirements lean.

<br />

**Table of contents**
* [Requirements](#requirements)
  * [Geth Chaindata Disk Requirements](#geth-chaindata-disk-requirements)
  * [Parity Chaindata Disk Requirements](#parity-chaindata-disk-requirements)
* [Linux Setup](#linux-setup)
* [Setting Up A Go Etherem Node For The ETH Chain](#setting-up-a-go-etherem-node-for-the-eth-chain)
  * [Install Geth](#install-geth)
  * [Geth Maintenance](#geth-maintenance)
  * [Setup Geth Service](#setup-geth-service)
  * [Using The Geth Service](#using-the-geth-service)
  * [Geth Blockchain Data Maintenance](#geth-blockchain-data-maintenance)
* [Setting Up A Parity Node On The ETH Or ETC Chains](#setting-up-a-parity-node-on-the-eth-or-etc-chains)
  * [Install Parity](#install-parity)
  * [Parity Maintenance](#parity-maintenance)
  * [Setup Parity Service For The ETH Chain](#setup-parity-service-for-the-eth-chain)
  * [Setup Parity Service For The ETC Chain](#setup-parity-service-for-the-etc-chain)
  * [Using The Parity Service On The ETH Chain](#using-the-parity-service-on-the-eth-chain)
  * [Using The Parity Service On The ETC Chain](#using-the-parity-service-on-the-etc-chain)
  * [Parity Blockchain Data Maintenance For The ETH Chain](#parity-blockchain-data-maintenance-on-the-eth-chain)
  * [Parity Blockchain Data Maintenance For The ETC Chain](#parity-blockchain-data-maintenance-on-the-etc-chain)

<br />

<hr />

## Requirements

Some minimum requirements. These are just conservatives estimates:
* 4 GB RAM
* 2 CPU threads
* 4 GB swap file
* 40 GB SSD drive

### Geth Chaindata Disk Requirements

Here is the disk usage for a fresh-ish `--fast` ETH chain:

    $ du -hs chaindata/
    19G    chaindata/

### Parity Chaindata Disk Requirements

Here are the disk usage for fresh-ish ETH and ETC `--warp` chains:

    $ du -hs classic/ ethereum/
    7.8G    classic/
    8.8G    ethereum/

## Linux Setup
* Set up a non-root user, with sudo rights
* Remove root login via ssh

<br />

<hr />

## Setting Up A Go Etherem Node For The ETH Chain

### Install Geth

From https://github.com/ethereum/go-ethereum/wiki/Installation-Instructions-for-Ubuntu:

    $ sudo apt-get install software-properties-common
    $ sudo add-apt-repository -y ppa:ethereum/ethereum
    $ sudo apt-get update
    $ sudo apt-get install ethereum

    $ which geth
    /usr/bin/geth

### Geth Maintenance

    $ sudo apt-get update
    $ sudo apt-get upgrade

### Setup Geth Service

Set up the following systemd service:

    $ vi /etc/systemd/system/geth.service
    [Unit]
    Description=Geth
    
    [Service]
    Type=simple
    User={your username}
    Restart=always
    ExecStart=/usr/bin/geth --rpc 
    
    [Install]
    WantedBy=default.target

### Using The Geth Service

    # Start service
    sudo systemctl start geth
    # Stop service
    sudo systemctl stop geth
    # View all logs
    sudo journalctl -u geth
    # Tail log
    sudo journalctl -f -u geth

### Geth Blockchain Data Maintenance

* Stop the Geth service
* Remove the `$HOME/.ethereum/geth/chaindata` directory periodically or run `geth removedb`
* Start the Geth Service and it will fast sync

<br />

<hr />

## Setting Up A Parity Node On The ETH Or ETC Chains

### Install Parity

From https://github.com/paritytech/parity/releases, download the Linux x86_64 .deb file. For example:

    $ wget http://d1h4xl4cr1h0mo.cloudfront.net/v1.6.6/x86_64-unknown-linux-gnu/parity_1.6.6_amd64.deb
    $ sudo apt install ./parity_1.6.6_amd64.deb

    $ which parity
    /usr/bin/parity

### Parity Maintenance

* Manually update the parity binaries

### Setup Parity Service For The ETH Chain

Set up the following systemd service:

    $ vi /etc/systemd/system/parity.service
    [Unit]
    Description=Parity
    
    [Service]
    Type=simple
    User={your username}
    Restart=always
    ExecStart=/usr/bin/parity --warp --port 30303 --jsonrpc-port 8545 --no-dapps --no-ui
    
    [Install]
    WantedBy=default.target

### Setup Parity Service For The ETC Chain

Set up the following systemd service:

    $ cat /etc/systemd/system/parityclassic.service
    [Unit]
    Description=Parity Classic
    
    [Service]
    Type=simple
    User={your username}
    Restart=always
    ExecStart=/usr/bin/parity --chain classic --warp --port 40404 --jsonrpc-port 9545 --no-dapps --no-ui
    
    [Install]
    WantedBy=default.target

### Using The Parity Service On The ETH Chain

    # Start service
    sudo systemctl start parity
    # Stop service
    sudo systemctl stop parity
    # View all logs
    sudo journalctl -u parity
    # Tail log
    sudo journalctl -f -u parity

### Using The Parity Service On The ETC Chain

    # Start service
    sudo systemctl start parityclassic
    # Stop service
    sudo systemctl stop parityclassic
    # View all logs
    sudo journalctl -u parityclassic
    # Tail log
    sudo journalctl -f -u parityclassic

### Parity Blockchain Data Maintenance On The ETH Chain

* Stop the Parity service
* Remove `$HOME/.local/share/io.parity/ethereum/chains/ethereum`
* Start the Parity service

### Parity Blockchain Data Maintenance On The ETC Chain

* Stop the Parity service
* Remove `$HOME/.local/share/io.parity/ethereum/chains/classic`
* Start the Parity service
