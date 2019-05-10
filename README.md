# bcx-2019
This is the official documentation of the ZkSystems Technology for the Hackchallenges on the BCX 2019. 

## JSON-RPC Interface

This package provides a JSON-RPC interface to a blockchain node. Clients (i. e. peripherals connected to the node) can call the following methods:

* **sendMessage:** Send a message that will be broadcasted to the peer to peer network.
* **getBalance:** Get the balance of a given wallet address.
* **sendTransaction:** Send a transaction to the blockchain.

### Starting the JSON-RPC Server
The JSON-RPC server is started if you specify a port for it (`--json-rpc-port`). To start with a valid DAG state provide the `--dag` parameter. Have your wallet private key loaded from a JSON file by setting the `--keypair` parameter:

```sh
$ node src/ --json-rpc-port 3003 --keypair data/peer0_key.json --dag data/DAG.json 
```

### Testing with the Reference Client
There is a simple reference client that sends some JSON-RPC messages and displays the responses:

```sh
$ node json_rpc_client.js --host localhost:3003
```

### Sending JSON-RPC messages via cURL

```sh
$ curl -H 'Content-type: application/json' -d '{"jsonrpc": "2.0", "method": "sendMessage", "id": "1a2b3c", "params": {"message": "Here’s a message!"}}' http://localhost:3003/
```

```sh
$ curl -H 'Content-type: application/json' -d '{"jsonrpc": "2.0", "method": "getBalance", "id": "1a2b3d", "params": {"address": "04f36c6692c71a91d3fd041e49dfbc64cf2011b39cc2f16fc2f160fed73c1534e16e45aa735ccb6d91bafb41e2e2580578da7f80375aee0f924846cbbb0a03228d"}}' http://localhost:3003/
```

```sh
$ curl -H 'Content-type: application/json' -d '{"jsonrpc": "2.0", "method": "sendTransaction", "id": "1a2b3e", "params": {"toAddress": "04f36c6692c71a91d3fd041e49dfbc64cf2011b39cc2f16fc2f160fed73c1534e16e45aa735ccb6d91bafb41e2e2580578da7f80375aee0f924846cbbb0a03228d", "amount": 23, "payload": "Lorem"}}' http://localhost:3003/
```
