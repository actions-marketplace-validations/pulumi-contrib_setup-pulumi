# setup-pulumi

[![Test](https://github.com/pulumi-contrib/setup-pulumi/actions/workflows/test.yml/badge.svg)](https://github.com/pulumi-contrib/setup-pulumi/actions)
[![Hygiene](https://github.com/pulumi-contrib/setup-pulumi/actions/workflows/hygiene.yml/badge.svg)](https://github.com/pulumi-contrib/setup-pulumi/actions)
[![CodeQL](https://github.com/pulumi-contrib/setup-pulumi/actions/workflows/codeql.yml/badge.svg)](https://github.com/pulumi-contrib/setup-pulumi/actions)

Set up and cache the Pulumi CLI.

## Roadmap

This action aims to provide lower-level functionalities than the official
action.

## Usage

Currently, the semantic versioning style does not support to specify the version
of the packer itself. ​If you want to use a version other than the latest one,
be sure to specify the exact version.

### Example workflow

```yml
name: Pulumi

on:
  - pull_request
  - push

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Use latest Pulumi
        uses: pulumi-contrib/setup-pulumi@v1

      # or

      - name: Use latest Pulumi
        uses: pulumi-contrib/setup-pulumi@v1
        with:
          pulumi-version: v2.19.0
```

### ​How to specify the version of the action itself

There is a point that is particularly easy to misunderstand. It's where you
specify the version of the action _itself_.

```yml
- name: Use latest Pulumi
  uses: pulumi-contrib/setup-pulumi@v1
  #                                ^^^
```

We recommend that you include the version of the action. We adhere to
[semantic versioning](https://semver.org), it's safe to use the major version
(`v1`) in your workflow. If you use the master branch, this could break your
workflow when we publish a breaking update and increase the major version.

```yml
steps:
  # Reference the major version of a release (most recommended)
  - uses: pulumi-contrib/setup-pulumi@v1
  # Reference a specific commit (most strict)
  - uses: pulumi-contrib/setup-pulumi@b9dd0b6
  # Reference a semver version of a release (not recommended)
  - uses: pulumi-contrib/setup-pulumi@v1.0.0
  # Reference a branch (most dangerous)
  - uses: pulumi-contrib/setup-pulumi@master
```

## Inputs

- `pulumi-version`: Version of the Pulumi CLI to install (default `latest`)
