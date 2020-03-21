---
title: NPM basic commands
categories:
excerpt: List of basic npm commands you can use
tags:
toc: true
toc_sticky: true
author_profile: true
comments: true
---

### Package Management

| Command | Description |
| ------- | ----------- |
| `npm install <package-name>` | Install package locally |
| `npm install <package-name> -g` | Install package globally |
| `npm uninstall <package-name>` | Uninstall local package |
| `npm uninstall <package-name> -g` | Uninstall global package |

### Listing and searching

| Command | Description |
| ------- | ----------- |
| `npm ls` | List local packages |
| `npm ls -l` | List local packages with details |
| `npm ls -g` | List global packages |
| `npm ls -gl` | List global packages with details |
| `npm view` | List latest versions of local packages|
| `npm outdated` | List local packages which are outdated|
| `npm search <search-terms>` |Search the registry for packages matching the search terms|

### Updating

| Command | Description |
| ------- | ----------- |
| `npm update` | Update local production packages |
| `npm update --dev` | Update dev packages |
| `npm update -g` | Update global packages |
| `npm update <package-name>` | Update specific package |
