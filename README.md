# ChRIS Plugin Upload Action

[![test](https://github.com/FNNDSC/upload-chris-plugin/actions/workflows/test.yml/badge.svg)](https://github.com/FNNDSC/upload-chris-plugin/actions/workflows/test.yml)
[![MIT License](https://img.shields.io/github/license/fnndsc/upload-chris-plugin)](https://github.com/FNNDSC/upload-chris-plugin/blob/main/LICENSE)

A Github Action for publishing a ChRIS plugin to _ChRIS_.

## Quick Example

```yaml
name: publish

on:
  push:
    tags: [ '**' ]

jobs:
  upload:
    runs-on: ubuntu-latest
    steps:
      - name: Upload ChRIS plugin
        uses: FNNDSC/upload-chris-plugin@master
        with:
          dock_image: ghcr.io/fnndsc/pl-pluginname:1.2.3
          username: chris
          password: chris1234
          compute_names: host,nerc,hpc
```

For a complete example, see [./.github/workflows/test.yml](./.github/workflows/test.yml) or
https://github.com/FNNDSC/python-chrisapp-template/blob/main/.github/workflows/ci.yml

## Usage

`FNNDSC/upload-chris-plugin` uploads the JSON description of a _ChRIS_ plugin to a _ChRIS_ URL.
The description can be provided one of three ways:

1. As a JSON string `description_json`
2. As a path to a file `description_file`
3. Automatically from a Python-based _ChRIS_ plugin using using [`chris_plugin>=0.3.0`](https://pypi.org/project/chris-plugin/), given `dock_image`

In addition to one of `description_json`, `description_file`, or `dock_image`,
the variables `username` and `password` are also required.

By default, plugins are uploaded to https://cube.chrisproject.org/api/v1/.
The CUBE address can be changed by setting `chris_url`.

Other configurations are described in [./action.yml](./action.yml).
