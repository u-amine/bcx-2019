# bcx-2019
This is the official documentation of the ZkSystems Technology for the Hackchallenges on the BCX 2019. 

## JSON-RPC Interface

On a test network we run four blockchain nodes that expose a JSON-RPC. Clients (i. e. peripherals connected to the node) can call the following methods:

* **createWallet:** Create a new key pair. The public key becomes your wallet address.
* **sendTransaction:** Send a transaction to the blockchain.
* **getDAG:** Get the set of vertices in the DAG (did we mention our data structure is actually a [DAG](https://en.wikipedia.org/wiki/Directed_acyclic_graph), not a chain?).
* **getBalance:** Get the balance of a given wallet address.

### The JSON-RPC Server
There is an HTTPS JSON-RPC server listening on port 8545 on each of the following machines:

* bcx-1: 130.61.92.142
* bcx-2: 130.61.56.127
* bcx-3: 130.61.89.111
* bcx-4: 130.61.57.122

### Methods

**createWallet**
* params: []
* result: { publicKey _(string)_, privateKey _(string)_ }

**sendTransaction**
* params: toAddress _(string)_, amount _(number)_, payload _(string)_
* result: confirmation _or_ error

**getDAG**
* params: []
* result: set of vertices _(array)_

**getBalance**
* params: address _(string)_
* result: balance of the given address _(number)_

### Sending JSON-RPC messages via cURL

```sh
$ curl -H 'Content-type: application/json' -d '{"jsonrpc": "2.0", "method": "getBalance", "id": "1a2b3d", "params": {"address": "04f36c6692c71a91d3fd041e49dfbc64cf2011b39cc2f16fc2f160fed73c1534e16e45aa735ccb6d91bafb41e2e2580578da7f80375aee0f924846cbbb0a03228d"}}' https://130.61.….…:8545/ -k
```
(You need to tell cURL to [ignore certificate warnings](https://serverfault.com/questions/469824/curl-disable-certificate-verification) (the `-k` option) since there are only self-signed certificates on the nodes.)

```sh
$ curl -H 'Content-type: application/json' -d '{"jsonrpc": "2.0", "method": "sendTransaction", "id": "1a2b3e", "params": {"toAddress": "04f36c6692c71a91d3fd041e49dfbc64cf2011b39cc2f16fc2f160fed73c1534e16e45aa735ccb6d91bafb41e2e2580578da7f80375aee0f924846cbbb0a03228d", "amount": 23, "payload": "Lorem"}}' https://130.61.….…:8545/ -k
```
