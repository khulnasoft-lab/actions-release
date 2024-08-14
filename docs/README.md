## Usage

```yaml
name: Publish Release
on:
  push:
    tags:
      - 'v*'
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Create a Release
      uses: khulnasoft-lab/actions-release@master
      env:
        GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      with:
        title: MyReleaseMessage
```

## Mandatory Arguments

### title
`title` is a message which should appear in the release. May contain spaces.

## Optional Arguments

### workdir
`workdir` can be used to specify a directory that contains the repository to be published. 

## Notes

`${{ secrets.GITHUB_TOKEN }}` can be used for publishing, if you configure the correct permissions.

This can be done by giving the Github token _all_ permissions (referred to as "Read and write permission") with the setting below available in Settings > Actions > General  

OR alternatively it can be achieved via adding

```yaml
permissions:
  packages: write
  contents: write
```
