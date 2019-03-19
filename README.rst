Ansible playbooks to setup Bitcoin-core and Go-Ethereum on Ubuntu
=================================================================

Bitcoin-core setup
------------------

Provisioning:

.. code :: bash

    cd playbooks
    # Manually install ansible pre-requisites for Ubuntu 16.04 ...
    ssh REMOTE_HOST "sudo apt-get install python-minimal aptitude -y"
    ansible-playbook -v -i hosts --limit=bitcoin-core bicoin-core-provisioning.yml

Check:

.. code :: bash

    ssh btc01@wallet-btc01 "bitcoin-cli getblockcount"

    ssh btc01@wallet-btc01 "tail -f ~/.bitcoin/debug.log"

References:

    - `Bitcoin Core integration/staging tree <https://github.com/bitcoin/bitcoin>`_
    - `UNIX BUILD NOTES <https://github.com/bitcoin/bitcoin/blob/master/doc/build-unix.md>`_
    - `Bitcoin Developer Examples <https://bitcoin.org/en/developer-examples#testing-applications>`_
    - `Learning-Bitcoin-from-the-Command-Line <https://github.com/ChristopherA/Learning-Bitcoin-from-the-Command-Line/blob/master/03_1_Verifying_Your_Bitcoin_Setup.md>`_


Go-ethereum setup
-----------------

Provisioning:

.. code :: bash

    cd playbooks
    # Manually install ansible pre-requisites for Ubuntu 16.04 ...
    ssh REMOTE_HOST "sudo apt-get install python-minimal aptitude -y"
    ansible-playbook -v -i hosts --limit=go-ethereum go-ethereum-provisioning.yml

then you can start you node running:

.. code :: bash

    cd $HOME/go-ethereum
    build/bin/geth

and in another client session:

.. code :: bash

    geth attach
    > eth.syncing
    {
      currentBlock: 114218,
      highestBlock: 493543,
      knownStates: 48436,
      pulledStates: 45936,
      startingBlock: 85702
    }
    > eth.blockNumber
    0
    > admin.nodeInfo
    {
      enode: "enode://4a6bef74d1bec5096e82d7321e81fbb9cc22fd711747de1d6d58d0d262ab229ad220f2c9ac42a21289348dbb6cffd3dcb736c638f099c49cae25cbcc92574d53@[::]:30303",
      id: "4a6bef74d1bec5096e82d7321e81fbb9cc22fd711747de1d6d58d0d262ab229ad220f2c9ac42a21289348dbb6cffd3dcb736c638f099c49cae25cbcc92574d53",
      ip: "::",
      listenAddr: "[::]:30303",
      name: "Geth/v1.7.3-stable-4bb3c89d/linux-amd64/go1.9",
      ports: {
        discovery: 30303,
        listener: 30303
      },
      protocols: {
        eth: {
          difficulty: 17179869184,
          genesis: "0xd4e56740f876aef8c010b86a40d5f56745a118d0906a34e69aec8c0db1cb8fa3",
          head: "0xd4e56740f876aef8c010b86a40d5f56745a118d0906a34e69aec8c0db1cb8fa3",
          network: 1
        }
      }
    }
    >

List transactions:

    > eth.getBlock(eth.blockNumber, true).transactions


See also:

    - http://etherscan.io

Smart contracts:

    - https://etherscan.io/tokens

References:

    - `Official Go implementation of the Ethereum protocol <https://github.com/ethereum/go-ethereum>`_
    - `Installation Instructions for Ubuntu <https://github.com/ethereum/go-ethereum/wiki/Installation-Instructions-for-Ubuntu>`_
    - `How to Install Go 1.9 on Ubuntu <https://tecadmin.net/install-go-on-ubuntu/>`_

