---
title: aws.env
sidebarHeader: Reference
sidebarSubHeader: Airnode
basePath: /airnode/latest/deployment-files/
outline: deep
tags:
---

<VersionWarning/>

<PageHeader>v1.0 → Deployment Files </PageHeader>

# {{$frontmatter.title}}

When it is time to deploy the Airnode to AWS, the Docker
[deployer image](../../grp-providers/docker/deployer-image.md) will need the AWS
credentials to build the node.

- Variable names cannot contain dashes (-) or start with a number.

```bash
AWS_ACCESS_KEY_ID=XYZ...123
AWS_SECRET_ACCESS_KEY=ABC7...89
```