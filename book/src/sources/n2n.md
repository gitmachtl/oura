# Node-to-Node

The Node-to-Node (N2N) source uses Ouroboros mini-protocols to connect to a local or remote Cardano node through a tcp socket bearer and fetches block data using the ChainSync mini-protocol instantiated to "headers only" and the BlockFetch mini-protocol for retrieval of the actual block payload.

## Configuration

The following snippet shows an example of how to setup a typical N2N source:

```toml
[source]
address = ["Tcp", "<hostname:port>"]
magic = <network magic>
since = [<slot>, "<block hash>"]

[source.mapper]
include_transaction_details = <bool>
```

### Section `source`:

- `type`: this field must be set to the literal value `N2N`
- `address`: a tuple describing the location of the tcp endpoint It must be specified as a string with hostname and port number.
- `magic`: the magic of the network that the node is running (`mainnet`, `testnet` or a custom numeric value)
- `since`: the point in the chain where reading of events should start from. It must be specified as a tuple of slot (integer) and block hash (hex string)

### Section `source.mapper`

This section provides options to tweak the behaviour of how raw chain data is mapped into _Oura_ events.

- `include_transaction_details`: instructs the mapper to include all details in the transaction event payload (inputs, outputs, metadata, mint, etc)

## Examples

Connecting to a local Cardano node in mainnet through unix sockets:

```toml
[source]
type = "N2N"
address = ["Tcp", "relays-new.cardano-mainnet.iohk.io:3001"]
magic = "mainnet"
```

Connecting to a local Cardano node in testnet through unix sockets:

```toml
[source]
type = "N2N"
address = ["Tcp", "relays-new.cardano-mainnet.iohk.io:3001"]
magic = "testnet"
```

Start reading from a particular point in the chain:

```toml
[source]
type = "N2C"
address = ["Tcp", "relays-new.cardano-mainnet.iohk.io:3001"]
magic = "mainnet"
since = [48896539, "5d1f1b6149b9e80e0ff44f442e0cab0b36437bb92eacf987384be479d4282357"]
```

Include all details inside the transaction events:

```toml
[source]
type = "N2N"
address = ["Tcp", "relays-new.cardano-mainnet.iohk.io:3001"]
magic = "mainnet"


[source.mapper]
include_transaction_details = true
```
