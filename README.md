# Build & Install Cadius Action

This action will build and install the Cadius tool for creating and modifying Apple II ProDOS disk images.

* The tip-of-tree version from https://github.com/mach-kernel/cadius is used.
* Cadius is built and installed, so later steps can use `cadius` commands directly.

The action has no inputs or outputs. 

## Example

```yml
name: build
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: a2stuff/build-install-cadius-action@v1
      - name: build and package
        run: |
          make
          cp out/built.BIN "out/BUILT#062000"
          cadius CREATEVOLUME image.po VOLNAME 140KB 
          cadius ADDFILE image.po /VOLNAME "out/BUILT#062000"
          cadius CATALOG image.po
```
