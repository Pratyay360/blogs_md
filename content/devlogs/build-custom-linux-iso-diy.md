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
  - bootc
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
> Example:      `${{ secrets.COSIGN_PRIVATE_KEY }}`
>
> ### `cosign_public_key:` **(optional)**
>
> The public key, but passed as env.
>
> Example:      `${{ secrets.COSIGN_PUBLIC_KEY }}`
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
> Example:      `${{ github.token }}`
>
> Default: “
>
> ### `registry_username:` **(optional)**
>
> The username used to sign into the container registry.
>
> Default:      `${{ github.repository_owner }}`
>
> ### `pr_event_number:` **(required)**
>
> The event number used to tag images pushed from pull requests.
>
> Example:      `${{ github.event.number }}`
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
> Default:      `${{ github.repository_owner }}`
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

```bash
.
├── common.sh
├── extract-image-name.sh
├── generate-iso.sh
├── upload.sh
├── view-upload.sh
└── write-job-summary.sh

```

list of scripts 

1. `.github/scripts/common.sh`

```bash
#!/usr/bin/env bash
# Shared helpers for the ISO workflow scripts. Source this; never run it directly.

set -euo pipefail

log() { printf '%s\n' "$*"; }
warn() { printf '::warning::%s\n' "$*"; }
error() { printf '::error::%s\n' "$*" >&2; }

die() {
  error "$*"
  exit 1
}

# require_env NAME [NAME...] - fail with one clear message per missing variable.
require_env() {
  local name
  for name in "$@"; do
    [[ -n "${!name:-}" ]] || die "Missing required environment variable: $name"
  done
}

# github_output "key=value" - write a step output when running in Actions,
# print it locally otherwise.
github_output() {
  if [[ -n "${GITHUB_OUTPUT:-}" ]]; then
    printf '%s\n' "$1" >> "$GITHUB_OUTPUT"
  else
    log "[output] $1"
  fi
}

# step_summary "line" - append a line to the job summary when running in
# Actions, print it locally otherwise.
step_summary() {
  if [[ -n "${GITHUB_STEP_SUMMARY:-}" ]]; then
    printf '%s\n' "$1" >> "$GITHUB_STEP_SUMMARY"
  else
    log "$1"
  fi
}
```

2. `.github/scripts/extract-image-name.sh`

```bash
#!/usr/bin/env bash
# Derive a short ISO name from a fully qualified image reference.

SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
source "$SCRIPT_DIR/common.sh"

require_env IMAGE

BASENAME="${IMAGE##*/}"
NAME="${BASENAME%:*}"

[[ -n "$NAME" ]] || die "Could not derive a name from IMAGE=$IMAGE"

log "Image: $IMAGE -> name: $NAME"
github_output "name=$NAME"
```

3. `.github/scripts/generate-iso.sh`

```bash
#!/usr/bin/env bash
# Build an ISO for a published container image and normalize its output path.

SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
source "$SCRIPT_DIR/common.sh"

require_env IMAGE NAME

OUTPUT_DIR="${OUTPUT_DIR:-$(pwd)/output}"
mkdir -p "$OUTPUT_DIR"
OUTPUT_DIR="$(cd "$OUTPUT_DIR" && pwd)"
ISO_PATH="$OUTPUT_DIR/${NAME}.iso"

log "Generating ISO: image=$IMAGE name=$NAME output=$OUTPUT_DIR"

for tag in latest v1.4.0; do
  if ! podman pull "ghcr.io/jasonn3/build-container-installer:${tag}"; then
    warn "Warm-up pull of ${tag} failed; continuing."
  fi
done

if ! bluebuild generate-iso --iso-name "${NAME}.iso" --output-dir "$OUTPUT_DIR" image "$IMAGE"; then
  warn "bluebuild generate-iso failed; retrying once with VERSION=42 (lorax fallback)."
  VERSION=42 bluebuild generate-iso --iso-name "${NAME}.iso" --output-dir "$OUTPUT_DIR" image "$IMAGE"
fi

if [[ ! -f "$ISO_PATH" ]]; then
  mapfile -t candidates < <(find "$OUTPUT_DIR" -maxdepth 3 -type f -name '*.iso' | sort)
  if [[ ${#candidates[@]} -gt 0 ]]; then
    log "Expected $ISO_PATH; promoting ${candidates[0]} instead."
    cp -v "${candidates[0]}" "$ISO_PATH"
  fi
fi

[[ -f "$ISO_PATH" ]] || die "ISO not found at $ISO_PATH"

ls -lh "$ISO_PATH"
github_output "iso-output-path=$ISO_PATH"
```

4. `.github/scripts/upload.sh`

```bash
#!/usr/bin/env bash
# Upload an ISO to GoFile and emit a download URL plus QR code URL.
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
source "$SCRIPT_DIR/common.sh"

require_env FILE NAME IMAGE
[[ -f "$FILE" ]] || die "ISO file not found: $FILE"

# Extract a usable download URL from a GoFile API response.
response_url() {
  local url
  url="$(printf '%s' "$1" | jq -r '.data.downloadPage // .data.directLink // empty' 2>/dev/null || true)"
  if [[ -n "$url" && "$url" != "null" ]]; then
    printf '%s' "$url"
  fi
  return 0
}

TOKEN="${GOFILE_TOKEN:-${TOKEN:-}}"
log "Uploading $FILE ($(du -h "$FILE" | cut -f1)) to GoFile..."

RESPONSE=""
if [[ -n "$TOKEN" ]]; then
  RESPONSE="$(curl -sS --fail-with-body -X POST -F "file=@$FILE" -F "token=$TOKEN" \
    https://upload.gofile.io/uploadFile 2>&1)" || RESPONSE=""
  if [[ -z "$(response_url "$RESPONSE")" ]]; then
    RESPONSE="$(curl -sS --fail-with-body -X POST -F "file=@$FILE" \
      -H "Authorization: Bearer $TOKEN" https://upload.gofile.io/uploadFile 2>&1)" || RESPONSE=""
  fi
fi
if [[ -z "$(response_url "$RESPONSE")" ]]; then
  RESPONSE="$(curl -sS --fail-with-body -X POST -F "file=@$FILE" \
    https://upload.gofile.io/uploadFile 2>&1)" || RESPONSE=""
fi

log "GoFile response: $RESPONSE"
URL="$(response_url "$RESPONSE")"
[[ -n "$URL" ]] || die "Could not parse a download URL from the GoFile response."

QR_DATA="$(python3 -c 'import sys, urllib.parse; print(urllib.parse.quote(sys.argv[1], safe=""))' "$URL")"
QRCODE="https://api.qrserver.com/v1/create-qr-code/?size=256x256&data=${QR_DATA}"

github_output "url=$URL"
github_output "qrcode=$QRCODE"
log "GoFile URL: $URL"
log "GoFile QR:  $QRCODE"
```



&nbsp;

`iso-action.yaml`

```yaml
name: Build ISO and Upload

on:
  workflow_run:
    workflows: ["bluebuild"]
    types:
      - completed
  workflow_dispatch:

concurrency:
  group: iso-build-${{ github.ref || github.run_id }}
  cancel-in-progress: false

# Pinned tool version: change here to upgrade every ISO build at once.
env:
  BLUEBUILD_VERSION: "0.9.42"

jobs:
  iso:
    name: Build ISO
    runs-on: ubuntu-latest
    permissions:
      contents: write
      packages: write
    strategy:
      fail-fast: false
      matrix:
        images:
          - quay.io/pratyay360/catchy-kinoite:latest
          - quay.io/pratyay360/catchy-silverblue:latest
          - quay.io/pratyay360/catchy-sway:44
          - quay.io/pratyay360/catchy-cosmic:latest
          - quay.io/pratyay360/sway:44
          - quay.io/pratyay360/kinoite:latest
          - quay.io/pratyay360/silverblue:latest
          - quay.io/pratyay360/cosmic:latest

    # Every run step is a single script with a fixed contract: required inputs
    # are passed as env vars, results go to $GITHUB_OUTPUT or the job summary.
    steps:
      - name: Checkout repository
        uses: actions/checkout@main

      - name: Install toolchain
        run: ./.github/scripts/install-toolchain.sh

      - name: Extract image name
        id: recipe
        env:
          IMAGE: ${{ matrix.images }}
        run: ./.github/scripts/extract-image-name.sh

      - name: Generate ISO from published image
        id: generate-iso
        env:
          IMAGE: ${{ matrix.images }}
          NAME: ${{ steps.recipe.outputs.name }}
        run: ./.github/scripts/generate-iso.sh

      - name: Upload ISO to GoFile
        id: gofile
        env:
          FILE: ${{ steps.generate-iso.outputs.iso-output-path }}
          IMAGE: ${{ matrix.images }}
          NAME: ${{ steps.recipe.outputs.name }}
          GOFILE_TOKEN: ${{ secrets.GOFILE_TOKEN }}
        run: ./.github/scripts/upload.sh

      - name: View URL and QR Code
        if: always()
        env:
          ISO_FILE: ${{ steps.generate-iso.outputs.iso-output-path }}
          URL: ${{ steps.gofile.outputs.url }}
          QRCODE: ${{ steps.gofile.outputs.qrcode }}
        run: ./.github/scripts/view-upload.sh

      - name: Add job step summary
        env:
          NAME: ${{ steps.recipe.outputs.name }}
          IMAGE: ${{ matrix.images }}
          URL: ${{ steps.gofile.outputs.url }}
          QRCODE: ${{ steps.gofile.outputs.qrcode }}
        run: ./.github/scripts/write-job-summary.sh
```
