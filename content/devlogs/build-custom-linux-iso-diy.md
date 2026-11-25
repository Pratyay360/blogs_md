---
title: Build Custom Linux iso's diy
description: Generate custom Linux ISOs with custom bootc image and GitHub Actions
date: '2026-11-23T18:37:31Z'
draft: false
tags:
  - bluebuild
  - ublue
  - gofiles
  - github
  - iso
  - os
isCJKLanguage: false
headless: false
slug: build-custom-linux-iso-diy
---
## Prerequisites

You should already have a bootc container build CI pipeline based on the [BlueBuild workshop](https://workshop.blue-build.org/). This post starts after that image build works.

GitHub Actions has enough compute to build the image. Artifact storage is the weak point, so this workflow uploads the finished ISO to a separate file host.

![GitHub Actions storage limits](https://i.ibb.co/0p4PkZKF/image-png.png)

The ISOs in this project are usually 5 to 6 gigabytes on an average. That is too large for an Actions artifact.

![Example ISO size](https://i.ibb.co/Z1vLMRrM/image-png.png)

A small object storage will not cover a file size of 5 6 gigabytes it would be hell lot of expensive. I wanted something cheap and low maintenance (do once and forget), so this workflow uploads the finished ISO file to [GoFile](https://gofile.io/).



&nbsp;

## What the BlueBuild action does

The [BlueBuild GitHub Action reference](https://blue-build.org/reference/github-action/) Lists the inputs for the image build. The action publishes a container image, not an ISO. The ISO comes next, using that published image as its input.

> **blue-build/github-action**
>
> > **Note**
>
> This is an automatically generated reference page for the [BlueBuild GitHub Action](https://github.com/blue-build/github-action/).
>
> ## **Inputs**
>
> ### `recipe:` **(required)**
>
> The [recipe](https://blue-build.org/reference/recipe/) file to build the image from, relative to the `config/` or `recipes/` directory.
>
> Default: `recipe.yml`
>
> ### `cosign_private_key:` **(required)**
>
> The Sigstore/cosign secret used to sign the image.
>
> Example:    `${{ secrets.COSIGN_PRIVATE_KEY }}`
>
> ### `cosign_public_key:` **(optional)**
>
> The public key, but passed as env.
>
> Example:    `${{ secrets.COSIGN_PUBLIC_KEY }}`
>
> Default: “
>
> ### `push:` **(optional)**
>
> Whether to push the image to a container registry.
>
> Default: `true`
>
> ### `registry_token:` **(optional)**
>
> The token used to sign into the container registry.
>
> Example:    `${{ github.token }}`
>
> Default: “
>
> ### `registry_username:` **(optional)**
>
> The username used to sign into the container registry.
>
> Default:    `${{ github.repository_owner }}`
>
> ### `pr_event_number:` **(required)**
>
> The event number used to tag images pushed from pull requests.
>
> Example:    `${{ github.event.number }}`
>
> ### `maximize_build_space:` **(optional)**
>
> Whether to run the unwanted software remover to maximize build space in the GitHub builder. Disable this with ‘false’ if your image doesn’t take up a lot of space and you’d rather have shorter build times.
>
> Default: `true`
>
> ### `use_unstable_cli:` **(optional)**
>
> If true, this action pulls the `main` branch of blue-build/cli instead of the stable version the current action version is configured to use by default. This feature is useful for testing new features, but should not be used in production. Input must match the string ‘true’ for the unstable version to be used.
>
> Default: `false`
>
> ### `cli_version:` **(optional)**
>
> Set this with a tag, sha, or branch name for the blue-build/cli repo to use that particular version of the CLI tool. This will override the `use_unstable_cli` input for the action.
>
> ### `registry:` **(optional)**
>
> The container registry to push the built image to.
>
> Default: `ghcr.io`
>
> ### `registry_namespace:` **(optional)**
>
> The namespace on the registry to push to.
>
> Example: `ublue-os`
>
> Default:    `${{ github.repository_owner }}`
>
> ### `chunkah:` **(optional)**
>
> Uses Chunkah to rechunk the image, allowing for smaller images and smaller updates.
>
> This will increase the build-time and take up more space during build-time.
>
> Default: `false`
>
> ### `build_chunked_oci:` **(optional)**
>
> Uses `rpm-ostree compose build-chunked-oci` to rechunk the image, allowing for smaller images and smaller updates.
>
> This will increase the build-time and take up more space during build-time.
>
> Default: `false`
>
> ### `max_layers:` **(optional)**
>
> Maximum number of layers to use when rechunking with `build-chunked-oci`.
>
> Default: `128`
>
> ### `rechunk:` **(optional)**
>
> Rechunk the ostree-based result images with [github.com/hhd-dev/rechunk](https://github.com/hhd-dev/rechunk) for more efficient diffs and updates. (lower image size, better download speed, better update resuming)
>
> Will make your builds considerably slower. This is an experimental option, as it can cause issues with file permissions in some scenarios, so enable on your own risk.
>
> *Warning*: This option will be deprecated in the future.
>
> Default: `false`
>
> ### `rechunk_clear_plan:` **(optional)**
>
> Disregard previous build’s layer plan when rechunking.
>
> Default: `false`
>
> ### `use_cache:` **(optional)**
>
> Make use of layer cache by pushing the layers to the registry. Input must match the string ‘true’ for the step to be enabled.
>
> Default: `false`
>
> ### `retry_push_count:` **(optional)**
>
> The number of times to retry pushing the image.
>
> Default: `0`
>
> ### `squash:` **(optional)**
>
> Uses buildah to squash the build’s layers into a single layer. Use of this option disables cache. Conflicts with adding `--build-driver` or `--squash` to the build opts.
>
> Default: `false`
>
> ### `build_opts:` **(optional)**
>
> Provide options to the call to the BlueBuild CLI build command. If you use this with the squash input set to true and provide either of the `--build-driver` or `--squash` flags an error will occur and the action will not run.
>
> Default:
>
> ### `working_directory:` **(optional)**
>
> Changes working directory for whole build. For example, setting this to `./abc/` would cause for the recipe to be read from `./abc/recipes/recipe.yml`.
>
> Default: `./`
>
> ### `skip_checkout:` **(optional)**
>
> Set to true to skip doing the actions/checkout step. This allows you to checkout manually before calling bluebuild/github-action and to modify files (such as supplying build information to other scripts) before building.
>
> Default: `false`
>
> ### `verify_install:` **(optional)**
>
> Set to true verify the cosign signature for the Blue-Build cli
>
> Default: `false`
>
> ### `digestfile:` **(optional)**
>
> Filesystem path that digests of built images will be written to in JSON format.
>
> Example file format: `{"ghcr.io/blue-build/base-images/fedora-kinoite:latest": "sha256:abcdef..."}`
>
> Default: ““

create an account on [gofile.io](https://gofile.io/)   And store the API KEY securely as `GOFILE_TOKEN`

![apikey](https://i.ibb.co/yc0SwnVd/image-png.png)

Store the api key in repository secret 

![GoFile storage overview](https://i.ibb.co/GQDrgfbC/image-png.png)

and account id as  `GOFILE_ACCOUNT_ID`  

![accountid](https://i.ibb.co/GvXCKp0K/image-png.png)

![add secrets](https://i.ibb.co/LXFkPdWY/2026-11-25-01-46-21-p-m-Github-Demo.gif)
