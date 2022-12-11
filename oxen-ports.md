## Mainnet

**Oxend p2p port for where the blockchain messages etc are shared between nodes**

```jsx
inline constexpr uint16_t P2P_DEFAULT_PORT = 22022;
```

**Oxend RPC Port for sending RPC requests including remote nodes for wallets (oxend status)**

```jsx
inline constexpr uint16_t RPC_DEFAULT_PORT = 22023;
```

**ZMQ usage** 

```jsx
inline constexpr uint16_t ZMQ_RPC_DEFAULT_PORT = 22024;
```

**QNET port used by LokiMQ to send quorum messages between SNs quorums**

```jsx
inline constexpr uint16_t QNET_DEFAULT_PORT = 22025;
```

## Testnet

```jsx
inline constexpr uint16_t P2P_DEFAULT_PORT = 38156;
```

```jsx
inline constexpr uint16_t RPC_DEFAULT_PORT = 38157;
```

```jsx
inline constexpr uint16_t ZMQ_RPC_DEFAULT_PORT = 38158;
```

```jsx
inline constexpr uint16_t QNET_DEFAULT_PORT = 38159;
```

### Remote RPC Nodes

public.loki.foundation -> has both mainnet and testnet endpoints for wallets running remote nodes

#### mainnet
```
--daemon-address public-na.optf.ngo:22023
```

#### testnet
```
public.loki.foundation:38157
```
lokitestnet.com
