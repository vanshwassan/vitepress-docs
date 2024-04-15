---
title: Proxy contracts
sidebarHeader: Reference
sidebarSubHeader: dAPIs
pageHeader: Reference → dAPIs → Understanding dAPIs
path: /reference/dapis/understand/proxy-contracts.html
outline: deep
tags:
---

<PageHeader/>

<SearchHighlight/>

<FlexStartTag/>

# {{$frontmatter.title}}

Proxy contracts are generated and deployed by the
[API3 Market](https://market.api3.org) and allow for simple access to dAPIs by
any dApp. Access the API3 Market to easily deploy a proxy contract and use it to
read the value of its dAPI. Each proxy contract is linked to a single dAPI and
an OEV beneficiary on a particular network.

dApp owners use the address of a proxy contract to read dAPIs with the
[IProxy interface](/reference/dapis/understand/iproxy.md). See the guide
[Reading a dAPI proxy ](/guides/dapis/read-a-dapi/) for a complete working
example.

```
import "@api3/contracts/v0.8/interfaces/IProxy.sol";
...
(value, timestamp) = IProxy(proxyAddress).read();

```

![proxy-contracts.png](../assets/images/proxy-contracts.png)

### Proxy contract uniqueness

Each dApp has a unique proxy contract address that is linked to a dAPI and to
their OEV beneficiary address that they set while deploying it. For example, the
proxy contract for the self-funded dAPI
[ZIL/USD](https://market.api3.org/dapis/polygon-testnet/ZIL-USD) on the Mumbai
testnet has an address of `0x4a40Ed2Dbd51e655eD64371737C81883B0524eB2`.
Therefore, the dApp can call the ZIL/USD dAPI to get its value and timestamp
using its proxy contract address.

```solidity
(value, timestamp) = IProxy(0x4a40Ed2Dbd51e655eD64371737C81883B0524eB2).read();
```

<FlexEndTag/>
