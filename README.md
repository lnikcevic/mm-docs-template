# Documentation service

This project is used to produce all forms of documentation for the service.

The documentation is created using the [mm-docs](https://github.com/majkinetor/mm-docs) documentation system.

## Features

- Beautiful responsive design using the [material](https://squidfunk.github.io/mkdocs-material) theme
- Navigational bar, TOC, search and various rich presentation functionalities
- Rich diagrams and interface mockups using PlantUML
- Macros can be implemented using python
- PDF export for each page or full site
- Gitlab/Github repository connection for editing within a browser

## Prerequisites

- Docker installation.
  - For Windows Desktop use: `cinst docker-desktop`  
- PowerShell (optional, developer friendliness)

## Usage

Within Powershell use `Invoke-Build` (ib):

|        Command         |                                            Description                                             |
| ---------------------- | -------------------------------------------------------------------------------------------------- |
| `ib Build`             | Build static site                                                                                  |
| `ib Serve -aPort 8888` | Serve static site on port 8888 (default is 8000)<br>This enables concurent use on several projects |

Otherwise, run appropriate docker commands:

```sh
export image=majkinetor/mm-docs
export aPort=8888

#build
docker run --rm -v $PWD:/docs8 $image mkdocs build

#serve
docker run --rm -v $PWD:/docs --name docs-$aPort --detach -p $aPort:$aPort $image mkdocs serve --dev-addr 0.0.0.0:$aPort
```

For general usage of `mm-docs` system see its [README.md](zr-docs/README.mm-docs.md).

## Adding documents

- Add new markdown somewhre in the `source\docs` hierarchy
- To be visible in navigation, add to `source\mkdocs.yml` `nav` section, otherwise, the page is availalbe via direct link

## Notes

- In order to use internal [Gitlab Docker registry](/../container_registry), make sure daemon setting `insecure-registries` points to the `gitlab.mfin.trezor.rs:4567`. On Windows use tray icon and *Settings -> Daemon -> Advanced*.
- Behind the proxy, if you pull [Docker Hub](https://hub.docker.com) images, you need to setup proxy: *Settings -> Daemon -> Proxies*.