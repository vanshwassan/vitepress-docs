---
title: Monitor Airnode
sidebarHeader: Reference
sidebarSubHeader: Airnode
pageHeader: Reference → Airnode → v1.0 → Understanding Airnode
path: /reference/airnode/latest/understand/monitor.html
version: v1.0
outline: deep
tags:
---

<VersionWarning/>

<PageHeader/>

<SearchHighlight/>

# {{$frontmatter.title}}

## Cloud Provider Log Organization

Airnode logs or log groups are named similarly in AWS and GCP and include the
following hyphen-separated components: `airnode`, `<airnode short address>`,
`<stage>`, and `<airnode cycle stage or request type>`, for example,
`airnode-9e62180-tutorial-startCoordinator`. The possible Airnode cycle stages
or request types and the logs they contain are as follows:

- `startCoordinator`: Logs for chain provider initialization and request
  fetching
- `run`: Logs of API calls and withdrawals originating from blockchain requests
- `httpReq`: Logs for [HTTP gateway requests](./http-gateways.md)
- `httpSignedReq`: Logs for
  [HTTP signed data gateway requests](./http-gateways.md)

### AWS

Airnode logs are available in
[CloudWatch<ExternalLinkImage/>](https://console.aws.amazon.com/cloudwatch)
under Logs > Log groups. Note that for the HTTP gateways, AWS generates a unique
`requestId` for each request. These should not be confused with the `requestId`
of a request originating from a blockchain.

### GCP

Airnode logs are available in the
[Logs Explorer<ExternalLinkImage/>](https://console.cloud.google.com/logs/). It
can be convenient to query or stream logs by the "Cloud Function" Resource Type
and then by "Function Name" in order to view a specific request type or Airnode
cycle stage.

## Local Airnode Client

Running the `airnode-client` Docker image will output container logs to the
command line. These logs are also available through the Docker interface e.g.
under Containers within Docker Desktop. See
[Airnode client image](../docker/client-image.md) for more information.