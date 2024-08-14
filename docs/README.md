## Usage

```
on:
  push:
    branches: [ main ]

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:

    - name: Get latest release of NodeJS
      uses: khulnasoft-lab/actions-release@master
      id: node_release
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        repository: "nodejs/node"
        type: "stable"

    - name: Build image
      uses: docker/build-push-action@v1
        with:
          ...
          dockerfile: Dockerfile
          tags: latest, ${{ steps.node_release.outputs.release }}
```

### Inputs

Name | Description | Example
--- | --- | ---
repository | The Github owner/repository | `nodejs/node`
type | The release type (prerelease | stable | latest | nodraft) | `stable`
token | Github auth token (default variable for each action session) | `${{ secrets.GITHUB_TOKEN }}`

#### Possible values for `type` input
* *stable* - Get the stable `latest` release
* *prerelease* - Get the latest `prerelease`
* *latest* - Get the *really* latest release with no matter is it stable or prerelease
* *nodraft* - Get the *really* latest release excluding drafts

### Outputs
Action outputs 3 variables
- `release` - release tag
- `release_id` - release Github ID
- `browser_download_url` - URL to download first file in release assets
