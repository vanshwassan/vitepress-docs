---
title: How dAPIs work
sidebarHeader: Reference
sidebarSubHeader: dAPIs
pageHeader: Reference → dAPIs → Understanding dAPIs
path: /reference/dapis/understand/index.html
outline: deep
tags:
---

<PageHeader/>

<SearchHighlight/>

<FlexStartTag/>

# {{$frontmatter.title}}

dAPIs are on-chain data feeds sourced from off-chain first-party oracles owned
and operated by API providers themselves and are continuously updated using
signed data. dApp owners can read the on-chain value of any dAPI in realtime.

dAPIs can serve a variety of continuously updated streams of off-chain data,
such as the latest cryptocurrency, stock, and commodity prices. They can power
various decentralized applications such as DeFi lending, synthetic assets,
stable coins, derivatives, NFTs, and more.

## Values stored on-chain

API providers, owners of first-party Airnodes, provide the signed data used to
store individual beacon values on-chain. A dAPI's value is in turn an aggregate
of beacon values. dAPI values are held in the
[Api3ServerV1.sol](https://github.com/api3dao/airnode-protocol-v1/blob/main/contracts/api3-server-v1/Api3ServerV1.sol)
contract.

<img src="../assets/images/beacons.png" style="width:80%;">

`Api3ServerV1.sol` manages the definitions for hundreds of dAPIs, each of which
is an aggregated value of multiple beacons or the value of a single beacon.

- Mainnet dAPIs: sourced from multiple data feeds (beacons). Available on
  Mainnets for production use.
- Testnet dAPIs: sourced from multiple data feeds (beacons). Available on
  Testnets for testing use.

Functions in `Api3ServerV1.sol` expose dAPIs values to API3 Market
[proxy contracts](/reference/dapis/understand/proxy-contracts.md). dApps do not
call the `Api3ServerV1.sol` contract directly but use intuitive proxy contracts
to get the value of a dAPI.

## The role of Airnode

Airnode is a flexible off-chain module that can support multiple protocols. Most
noticeably is its implementation of the request-response protocol (RRP) and data
feeds.

An Airnode is owned by an API provider and is used to call API provider
endpoints to fetch and sign data at the request of Airseeker. Airseeker uses the
signed data to determine if the deviation of a beacon value warrants an on-chain
update.

<img src="../assets/images/beacons-airnode.png">

In the diagram above, companies XYZ and ABC both provide ZIL/USD beacon values,
A and B, respectively, that are aggregated to determine the dAPI ZIL/USD value.
Airseeker regularly checks the deviation of ZIL/USD using the sign data from
these Airnodes. Airseeker will update the corresponding beacons behind ZIL/USD
when deviation is detected.

When a dApp requests the value of ZIL/USD, it will get the aggregated value of
the beacons behind the dAPI ZIL/USD.

## Availability

Both **Testnet dAPIs** and **Mainnet dAPIs** are available on the
[Market](https://market.api3.org/dapis).

| Testnet dAPIs                                                                   | Mainnet dAPIs                                  |
| ------------------------------------------------------------------------------- | ---------------------------------------------- |
| Single public [proxy contract](/reference/dapis/understand/proxy-contracts.md)  | Single public proxy contract                   |
| 1% deviation                                                                    | Multiple deviations<br/>(0.25%, 0.5%, 1%)      |
| 60 second [interval](/reference/dapis/understand/deviations.md#update-interval) | 30-60 second interval                          |
| 24 hour [heartbeat](/reference/dapis/understand/deviations.md#heartbeat)        | 2 minute or 24 hour heartbeat                  |
| Sourced from multiple<br/>data feeds (beacons)                                  | Sourced from multiple<br/>data feeds (beacons) |

<FlexEndTag/>
