# Helm Charts

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/soerenmetje)](https://artifacthub.io/packages/search?repo=soerenmetje)
[![Release Charts](https://github.com/soerenmetje/helm-charts/actions/workflows/release.yml/badge.svg)](https://github.com/soerenmetje/helm-charts/actions/workflows/release.yml)
[![Downloads](https://img.shields.io/github/downloads/soerenmetje/helm-charts/total?label=Downloads)](https://somsubhra.github.io/github-release-stats/?username=soerenmetje&repository=helm-charts)
[![Semantic Versioning](https://img.shields.io/badge/Semantic%20Versioning-2.0.0-yellow.svg?logo=semver)](https://semver.org/)


This repository contains a collection of my Helm charts to deploy applications on a Kubernetes cluster.
All charts of this repository can be inspected also on [Artifact Hub](https://artifacthub.io/packages/search?repo=soerenmetje&sort=relevance&page=1).

## Charts

| Name                                  | Description                                                                                                                              |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| [dolibarr](charts/dolibarr/README.md) | Web application to manage your company or foundation's activity (contacts, suppliers, invoices, orders, stocks, agenda, accounting, ...) |


## Sources
- Publish chart at Artifacthub: https://www.devopsschool.com/blog/helm-tutorial-how-to-publish-chart-at-artifacthub/
- GitHub action to publish a chart: https://github.com/helm/chart-releaser-action
- GitHub action to merge commits on main into gh-pages: https://github.com/everlytic/branch-merge
